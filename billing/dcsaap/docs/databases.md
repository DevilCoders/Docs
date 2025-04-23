База данных
===========

В проекте используются 2 бд:

- sqlite - для локального запуска и прогона тестов
- postgresql 12 - для dev/test/prod окружений

Если хочется запустить проект локально с postgresql, то:

```sh
# запускаем pg  в контейнере
➜ docker run --rm --name dcs-dev-pg -e POSTGRES_PASSWORD=qwerty -d -p 5432:5432/tcp postgres
9e739b1dab0d759479400a1d7e9ee488ed70e633f45db67d56207a242c47c658

➜ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
9e739b1dab0d        postgres            "docker-entrypoint.s…"   5 seconds ago       Up 3 seconds        0.0.0.0:5432->5432/tcp   dcs-dev-pg
```

Выставляем переменную окружения и запускаем проект:

```shell script
➜ export DEPLOY_ENVIRONMENT=development
➜ make dev-server
```

Остановка бд:

```shell script
➜ docker stop dcs-dev-pg
```
