### Админка базы данных сервиса
Production: https://admin.avia.yandex-team.ru

Testing: https://admin.avia.tst.yandex-team.ru

Репозиторий: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/admin

### Локальный запуск
Копируем файл с образцом переменных среды и редактируем его как надо.
```bash
cp ./tools/samples/environments.sh ./tools/environments.sh
vim ./tools/environments.sh
./tools/run-dev.sh
```

Для доступа к админскому интерфейсу у вас должны быть соответствующие права.
При запуске локально проще всего получить права админа, создав суперпользователя
и зайти в интерфейс админки под этим пользователем. Создать суперпользователя можно так:
```
./tools/run-manage.sh createsuperuser
```

Самый простой способ запустить gunicorn-приложение:
* Оставить в `./tools/environments.sh` следующие переменные окружения:
  1. Для того, чтобы gunicorn можно было использовать без nginx
    * BIND_ADDRESS=127.0.0.1:8000
  2. Для того, чтобы не возится с настройкой yandex-team авторизации
    * SKIP_AUTH=1
  3. Для того, чтобы статику раздавал тоже gunicorn, в этом случае статика соберется при запуске ```./tools/run-dev.sh```
    * ENABLE_DEV_STATIC=1
    * STATIC_ROOT="${ROOT}/bin/static/"
    * MEDIA_ROOT="${ROOT}/media/"

Альтернативный способ запуска админки локально:
* Заказать сертификат на `*.LOGIN.avia.dev.yandex-team.ru`: https://crt.yandex-team.ru/request/
* Прописать сертификат и ключ в nginx
* Настроить конфиг nginx. Пример: tools/samples/nginx.conf, в комментариях есть инструкция про статику

Пример env-файла для запуска приложения из докер контейнера:
```./tools/samples/admin_env.list```

### Облачный Mysql
Можно поднять временный mysql https://wiki.yandex-team.ru/avia/dev/services-table/mysql/

### Запуск скриптов
#### Запустить `manage.py shell`

Локально:
```
Y_PYTHON_ENTRY_POINT="travel.avia.admin.app:manage" ./tools/run-dev.sh shell
```

В проде/тестинге:
```
Y_PYTHON_ENTRY_POINT="travel.avia.admin.app:manage" /app/app shell
```

####Запуск произвольного скрипта на примере синхронизации с расписаниями

Локально:
```
Y_PYTHON_ENTRY_POINT="travel.avia.admin.avia_scripts.sync_with_rasp.sync_all:main" ./tools/run-dev.sh --exclude=settlement
```
Альтернатива  Y_PYTHON_ENTRY_POINT="travel.avia.admin.avia_scripts.sync_with_rasp.sync_all:main" ./bin/app --exclude=settlement


В проде/тестинге:

```
Y_PYTHON_ENTRY_POINT="travel.avia.admin.avia_scripts.sync_with_rasp.sync_all:main" /app/app --exclude=settlement
```


### Миграции
Официальная django документация:

https://docs.djangoproject.com/en/1.11/topics/migrations/

Локально:
```
Y_PYTHON_ENTRY_POINT="travel.avia.admin.app:manage" ./tools/run-dev.sh makemigrations
```

Как работать с миграциями в Аркадии можно прочитать и поправить на wiki:

https://wiki.yandex-team.ru/avia/dev/services-table/admin/#kakdelatnovyemigracii


### Обновление бинарника для AVIA_RUN_ADMIN_SCRIPT_BINARY

1. Коммитим изменения в админке.
2. Чекаутим: `/trunk/arcadia/sandbox`
3. Чекаутим код бинарных тасок: `./ya make --checkout -j0 sandbox/projects/avia/run_admin_script_binary`
4. На всякий случай обновляем админку: `./ya make --checkout -j0 travel/avia/admin`
5. Переходим в папку с кодом таски: `cd sandbox/projects/avia/run_admin_script_binary`
6. Получить токен YT если нужно https://oauth.yt.yandex.net
7. Собираем бинарник: `ya make -r --checkout --yt-store -j1`
8. Загружаем бинарник в sandbox: `./task_binary/task_binary run --owner AVIA --create-only --type AVIA_RUN_ADMIN_SCRIPT_BINARY --attr task_type=AVIA_RUN_ADMIN_SCRIPT_BINARY`
