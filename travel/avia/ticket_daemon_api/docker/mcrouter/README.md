# mcrouter
Настройки запуска mcrouter

## Переменные окружения
```
YANDEX_ENVIRONMENT_TYPE = (development|testing|production)
MCROUTER_WORKERS = 1
```

## Локальный запуск
Скопировать файл локальных переменных окружения:

```
cp dev/env.list.sample dev/env.list
```

Собрать контейнер (не обязательно)

```
docker build -t registry.yandex.net/avia/mcrouter .
```

Запустить контейнер

```
docker run -p 5000:5000 --env-file dev/env.list registry.yandex.net/avia/mcrouter
```
