# Нагрузочный стенд SPIRIT

Нагрузочный стенд располагается в [Y.Deploy](https://deploy.yandex-team.ru/stages/spirit-loadtesting/)

## Конфигурация деплой стенда
Стенд создается из файла конфигурации, лежащем в файле `spirit-loadtesting.yaml`
Для поднятия/обновления настроек стенда из файла в `Y.Deploy` можно воспользовать командой:
```bash
    ya tool dctl put stage spirit-loadtesting.yaml
```
Перед выполнением команды нужно заполнить все отсутствующие "delegation_token" поля,
которые убраны из соображений защиты токенов.

Стенд состоит из следующих машин
 - `checkrenderer` - машина с рендерилкой чеков
 - `darkspirit` - машина с `darkspirit`
 - `db` - полноценная `Oracle` база данных поднятая в `Deploy` для `darkspirit`
 - `loadmock` - Моки внешних сервисов, на текущий момент мокается сервис `MDS S3`
(Подробнее про `loadmock` [тут](https://a.yandex-team.ru/arc/trunk/arcadia/payplatform/spirit/loadtest/loadmock/README.md))
 - `whitespirit` - машина с `whitespirit`, в качестве касс используются `MockDevice`
 - `tank` - свой танк в `Y.Deploy` для удобной отладки (подробнее про танк и
тестовые сценарии [тут](https://a.yandex-team.ru/arc/trunk/arcadia/payplatform/spirit/loadtest/tank/README.md))

## Подготовка стенда
После поднятия стенда в деплой, база может сброситься, если были в размере диска или образе. Также
Информация `whitespirit` о кассах может быть не синхронизирована из-за того, что на стенде не
работает `cron` синхронизирующий информацию с `whitespirit`.
В таких случаях стрельбы покажут `HTTP` коды `500` или `0`.

### Накатка базы
Делается аналогично накатке при работе с докером:
 - Запустить DB в deploy
 - Создать виртуальное окружение локально или выполнять команды из докера с кодом `darkspirit`
```bash
virtualenv --python=/usr/bin/python2 dsvenv2
. dsvenv2/bin/activate
```
 - Убедиться что все зависимости установлены
```bash
pip install -r darkspirit/requirements.txt
pip install -r darkspirit/requirements_dev.txt
```
 - Инициализировать переменные окружения
```bash
export DB_NAME=db.arqsurvl3f5igple.sas.yp-c.yandex.net
export NLS_LANG="AMERICAN_CIS.UTF8"
export NLS_DATE_FORMAT="DD mon YYYY HH24:MI"
export NLS_SORT="RUSSIAN"
export NLS_LANG="AMERICAN_AMERICA.UTF8"
export NLS_NUMERIC_CHARACTERS=". "
```
 - Добавить скрипты накатки в `PATH`
```bash
export PATH=$PATH:darkspirit/docker/darkspirit/deploy-testing/usr/bin
```
 - Cтартовать скрипт накатки
```bash
run-liquibase darkspirit/sql-liquibase/sql/DS/
```

### Синхронизация whitespirit и darkspirit
Дернуть ручку синхронизации в `darkspirit`
```bash
curl -X POST http://service.rwqywsqtjmufxnr4.sas.yp-c.yandex.net/v1/admin/sync-cashregisters
```
Если касс много, запрос может отвалится по timeout, можно дернуть еще раз
