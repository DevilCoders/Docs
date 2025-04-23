Авиа статистика
=====

### Развернуть на дев-хосте:
Создать базу
```
mysql -u root -p
CREATE DATABASE avia_stats;
```

```
cp ./tools/samples/environments.sh ./tools/environments.sh
```

Для свеже созданной базы выполняем что бы создать схему
```
./tools/run-manage.sh migrate
```

Если пользователя ещё нет, то заводим через:
```
./tools/run-manage.sh createsuperuser
```

Самый простой способ запустить gunicorn-приложение:
* Оставить следующие переменные окружения:
  1. Для того, чтобы gunicorn можно было использовать без nginx
    * BIND_ADDRESS=127.0.0.1:8000
  2. Для того, чтобы не возится с настройкой yandex-team авторизации
    * DISABLE_AUTH_MIDDLEWARE=1
  3. Для того, чтобы статику раздавал тоже gunicorn, в этом случае статика соберется при запуске ```./tools/run-dev.sh```
    * ENABLE_DEV_STATIC=1
    * STATIC_ROOT="${ROOT}/bin/static/"

Альтернативный способ запуска:
* Заказать сертификат на `*.LOGIN.avia.dev.yandex-team.ru`: https://crt.yandex-team.ru/request/
* Прописать сертификат и ключ в nginx
* Настроить конфиг nginx. Пример: tools/samples/yandex-avia-stats.nginx, в комментариях есть инструкция про статику


Запускать: `./tools/run-dev.sh`
