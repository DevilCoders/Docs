Greenplum Manager (GPDBM) - это сервис для управления Greenplum Database (GPDB).

## Решаемые задачи
- Бэкапирование данных и метаданных в [S3-MDS](https://wiki.yandex-team.ru/mds/s3-api/)
- Отстрел невалидных запросов: по ресурсам и времени выполнения

## Описание
### Архитектура
![Schema](https://jing.yandex-team.ru/files/o-skrobuk/Schema.png)

### Компоненты
- API предоставляет ручки:
  - бэкапы: добавить объект в очередь на бэкап/рестор, удалить бэкап, список
    актуальных бэкапов
  - запросы (sql query): список запущенных, убить запрос
  - проверка живучести сервиса
- Celery - очередь и выполнение таска
- AWSCLI - Amazon клиент, с помощью которого обеспечивается потоковая загрузки
и выгрузка данных из S3-MDS, а так же удаление бэкапов
- PGDUMP - бэкапирование метаданных

### Дизайн
[Обсуждение дизайна в TAXIDWH-3670](https://st.yandex-team.ru/TAXIDWH-3670)


## ToDo
- Отстрел неавлидных запросов

## Запуск pytest
Для начала необходимо настроить окружение:
```
sudo apt-get update && sudo apt-get install -y python3 python3-pip python3-virtualenv
python3 -m pip install --upgrade pip setuptools
python3 -m pip install virtualenv
python3 -m virtualenv ~/.env-gpdb-manager
source ~/.env-gpdb-manager/bin/activate
python -m pip install -r requirements.txt
```
Конфиг для коннекта `~/gpdb-manager-for-pytest.yaml`:
```
GP_MANAGER:
  PGAAS:
    USER: -=LOGIN=-
    PASSWORD: -=PASSWORD=-

PGAAS:
  HOST: -=PGAAS_HOST=-

GP:
  BUTTHEAD:
    SSLMODE: require
    HOST: gpdb-pgbouncer.taxi.tst.yandex.net
    PORT: 5432
    DBASE: butthead
    USER: -=LOGIN=-
    PASSWORD: -=TOKEN=-
```
Запуск тестов с пометкой `fast`:
```
pytest -vv test -m "fast"
```
Запуск всех тестов:
```
pytest -vv test
```