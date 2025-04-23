Avia Backend
================

# Деплой
https://deploy.yandex-team.ru/projects/avia-backend

# Локальный запуск
После сборки бинарник будет в ``./bin/app/app`` от корня проекта.

Для работы нужна база mysql. Для взаимодействия с базой 
можно переопределить настройки через переменные окружения:
- ``AVIA_MYSQL_HOST``
- ``AVIA_MYSQL_DATABASE``
- ``AVIA_MYSQL_USER``
- ``AVIA_MYSQL_PASSWORD``

Также для работы нужны memcached  и MCRouter.

Установить MCRouter https://github.com/facebook/mcrouter#quick-start-guide

## Запуск
```bash
cp ./tools/samples/environments.sh ./tools/
vim ./tools/environments.sh
./tools/run-dev.sh
```

## Запуск manage.py
``Y_PYTHON_ENTRY_POINT="travel.avia.backend.app:manage" ./bin/app/app``
