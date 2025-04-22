# golp-docker-driver

Docker logs plugin for LogPusher

Плагины представляют из себя особым образом созданные Docker контейнеры, внутри которого находится исполняемый файл. Контейнер запускается в особом namespace Docker и имеет доступ к некоторым метаданным контейнера (env, id, limits, etc). Вместе с этим, контейнер-плагин - изолирован от хост машины. Плагин собранный для Linux не запустится под macos/win, для этого нужны разные плагины/бинарники внутри плагина. Также изоляция накладывает ограничения на доступ плагина к localhost.

## Build & Release
```
BINARY_VERSION=0.0.1 make test build-linux
BINARY_VERSION=0.0.1 make build-docker
```

## Usage

```
docker plugin install registry.vertis.yandex.net/golp-logger --alias golp-logger
# set params (optional)
docker plugin set GOLP_HOST=localhost:12345 LOG_LEVEL=debug
# enable plugin
docker plugin enable golp-logger
# run container
docker run -d --log-driver=golp-loger --log-opt service-name=svcname someimage
```

# Config

### Env vars

Задаются через `docker plugin set`

- GOLP_HOST (default: localhost:31321), адрес коннекта к лог-пушеру
- LOG_LEVEL (default: info) уровень логирования

### log-opts

Задаются через `--log-opt` к `docker run`

- golp-host (host:port для переопределения адреса пушера для конкретного контейнера)
- service-name (поле `_service` для лог-пушера)

### container env

Драйвер читает следующие переменные из окружения контейнера:

- NOMAD_JOB_NAME (и проставляет поле `_service` для лог-пушера)

# Remove plugin
```
docker plugin disable golp-logger
docker plugin rm golp-logger
```
