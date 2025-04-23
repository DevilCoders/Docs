# Миграции БД

Миграции работают через [pgmigrate](https://github.com/yandex/pgmigrate) (есть в pip)

## Как запускать

Через **bash**:
```bash
pgmigrate -c "$(eval "echo `cat aws_stable.conn`")" info
```

For my fellow **fish**ermen:
```bash
pgmigrate -c (bash -c "eval echo `cat aws_stable.conn`") info
```

Также, для работы команд нужна утилита `jq`, которую можно скачать через `apt`.

## Как работать

Научиться работать с `pgmigrate` можно в [туториале](https://github.com/yandex/pgmigrate/blob/master/doc/tutorial.md).
