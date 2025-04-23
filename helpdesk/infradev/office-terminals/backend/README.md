# Office Terminals Backend

## Зависимости

python 3.8

### Установка зависимостей

Для установки зависимостей используется `poetry install`

### Возможные ошибки

1. Не ставится psycopg2 на MacOS, решается командой `brew link openssl --force` и выставлением переменных в окружение.

## Запуск тестов

### Запускаем тесты

`docker-compose down --remove-orphans && docker-compose -f docker-compose.tests.yml up --build`

## Запуск

### В облаках

Требуется определить в облаке следующие переменные окружения

```
# Данные базы данных для Django
PGAAS_DB_HOST
PGAAS_DB_PORT
PGAAS_DB_NAME
PGAAS_DB_USER
PGAAS_DB_PASSWORD
# Данные для Redis
REDIS_HOST - хост с включенным Sentinel
REDIS_PORT
REDIS_DB_NAME
REDIS_DB_PASSWORD

# Данные для Django
YAUTH_ENABLED - Взвести флаг для включения авторизации через BlackBox
SECRET_KEY

# TVM
TVM_CLIENT_ID
TVM_CLIENT_SECRET

# Данные для Celery
CELERY_RESULT_DJANGO - установить флаг если требуется
    отправлять результаты тасков в Django DB, а не Redis
```

### Запуск локально

```bash
docker-compose up
```

### Запуск на dev тачке

```bash
docker context create dev
docker context update dev --docker host=ssh://$(whoami)@<fqdn-виртуалки>
docker context use dev
docker-compose up
```
