Общее описание
================
https://fb.yandex-team.ru

[Приложение в qloud](https://platform.yandex-team.ru/projects/tools/feedback)

Ограничения доступа в соответствии с https://cia.yandex-team.ru

Техническое описание
=====

Разработка
----------
Нужен docker-compose

```(bash)
# Собираем образы
docker-compose build

# Применяем миграции
docker-compose run --rm server feedback migrate

# Запуск проекта
docker-compose up server celery celery-beat
```

Тесты
-----
`¯\_(ツ)_/¯`


Сборка и деплой
------
```(bash)
releaser release
```

Сборка и деплой фронтового компонента:
```(bash)
releaser build -i feedback-static -v stable -f frontend.Dockerfile
releaser push -i feedback-static -v stable
releaser deploy -i feedback-static -v stable -c frontend
``` 

Базы
----
База — [MySQL-балансер](https://wiki.yandex-team.ru/tools/dev/qloud/balanser-nad-mysql/), 

Секреты
-------
[Пароли роботов](https://wiki.yandex-team.ru/KirillSibirev/will/secrets-cia/)

#### Алерты
В корне лежит конфиг .monitorado.yml

Дока https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/monitorado/README.md

#### Дашборд
https://yasm.yandex-team.ru/panel/feedback/
