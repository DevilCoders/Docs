# Сервис "Ученьки"
[Подробное описание](https://wiki.yandex-team.ru/jandekspoisk/sepe/dezhurnajasmena/uchenki/ )



# Гайд по поднятию dev окружения

## 1) Сначала добыть все нужные токены:
Через [секретницу](https://yav.yandex-team.ru/edit/secret/sec-01ehp4fjc1sb1schc0qg8z5zhk/explore/version/ver-01ehp4fjch3z2kky590q168cx6)
или самому:
- [Nanny token](https://nanny.yandex-team.ru/ui/#/oauth)
- [Startrek token](https://wiki.yandex-team.ru/tools/support/startrek/api/tokenfortracker)
- [Infra token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5dd9c4ae3ecd4e73942858d992f2f341) 
- [Stat token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=801af94c94e040848ebe206086a7a4e2)
- [Juggler token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=cd178dcdc31a4ed79f42467f2d89b0d0)
- [YT token](https://yt.yandex-team.ru/docs/gettingstarted#auth)

и добавить в переменные окружения:
```sh
export STARTREK_TOKEN=AQAD-....
export NANNY_TOKEN=AQAD-....
export STAT_TOKEN=AQAD-....
export INFRA_TOKEN=AQAD-....
export JUGGLER_TOKEN=AQAD-....
export YT_TOKEN=AQAD-....
```
Также по-хорошему нужен и TVM, но это необязательный шаг.
  #### Локальный TVM для календаря
- Получить себе локально TVM tool под нужную платформу [подробнее тут](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#kakzapustittvm-demona)
- Взять конфиг из секрета в yav и положить в файл ``./tvm/config``
- Сгенерировать TVM токен локальный командой ``xxd -l 16 -p /dev/urandom > ./tvm/tvm-token``
- Запускать можно скриптом ```./tvm/tvm.sh```
- Добавить `export TVM_TOOL_PORT=40000`

## 2) Создать базу (psql) либо подключиться к тестинговой
- Для подключения к тестинговой нужно отредачить конфиг, находящийся в `config/config.yaml`. Данные можно взять у кого-то из [ABC Uchenki](https://abc.yandex-team.ru/services/uchenki/). Также потребуется добавить в переменные окружения данные от БД:
    ```sh
    export DB_NAME=%имя%
    export DB_USER=%пользователь%
    export DB_PASS=%пароль%
    ```
- Для создания своей локальной гайд ниже:

    ```sql
    CREATE USER youruser;
    CREATE DATABASE uchenki_test_db OWNER youruser;
    ALTER USER youruser  WITH PASSWORD 'youruser_pass';
    ```

    Переходим в созданную БД
    ```
    \c uchenki_test_db
    ```

    Создаем схему
    ```sql
    CREATE SCHEMA uchenki AUTHORIZATION youruser;
    ```
    В своём dev-окружении пароль нужно положить в переменные окружения имя БД, логин , пароль к БД и OAUTH токены
    ```
    export DB_NAME=uchenki_test_db
    export DB_USER=youruser
    export DB_PASS=youruser_pass
    ```
    Cобираем бинарник через `ya make`  
    Запускаем через `./uchenki_exec gunicorn`  
    Логи в `uchenki.log`  

    ### Сдампить БД с престейбла
    За доступом обратиться к любому из [ABC Uchenki](https://abc.yandex-team.ru/services/uchenki/).  
    Развернуть в свою созданную локальную БД.

    ### Миграции создаются
    ```
    ./uchenki_exec db migrate
    ```
    и надо добавлять созданный файл в ya.make

    ### Накатить миграции на базу

    ```
    ./uchenki_exec db upgrade
    ```

### Итоговый список переменных окружения

```sh
export STARTREK_TOKEN=AQAD-....
export NANNY_TOKEN=AQAD-....
export STAT_TOKEN=AQAD-....
export INFRA_TOKEN=AQAD-....
export JUGGLER_TOKEN=AQAD-....
export YT_TOKEN=AQAD-....
export DB_NAME=....
export DB_USER=....
export DB_PASS=....
```
Получив все эти токены и данные можно сохранить их в файл и в дальнейшем быстро инициализировать переменные окружения.

### Запуск приложения
Добавить в конфиг файл `environment: development`, если отсутствует

```
./uchenki_exec gunicorn
```

# Фронт
- Лежит в директории `frontend`

# Деплой
- Выкатки происходят через аркадийный [CI](https://a.yandex-team.ru/projects/uchenki/ci/releases/timeline?dir=search%2Fmon%2Fuchenki&id=uchenki-backend-release)
- Сам сервис живет в [Deploy](https://deploy.yandex-team.ru/projects/uchenki)
