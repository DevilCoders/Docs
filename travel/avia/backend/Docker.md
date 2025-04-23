# Docker

Образ собран на основе базового образа ubuntu:bionic.

## Сборка

```
docker build -t registry.yandex.net/avia/avia-backend .
```

## Запуск

```
docker run -p 8080:80 --env-file ./docker/dev_env.list registry.yandex.net/avia/avia-backend
```

## Загрузка в репозиторий

```
docker push registry.yandex.net/avia/avia-backend
```

# Выкладка

## Переменные окружения

```
YANDEX_ENVIRONMENT_TYPE=(development|testing|production)
NGINX_WORKERS=($(NUM_CORES))
GUNICORN_WORKERS=(2-4 x $(NUM_CORES))
GUNICORN_MAX_REQUESTS=100
MCROUTER_WORKERS=($(NUM_CORES))
```
