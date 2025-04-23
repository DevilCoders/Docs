# Руководство разработчика

## Quickstart

```
cd sloth
nvm use
npm i
```

## Локальная разработка

Для разработки локально создайте файл `.env` в корне проекта и добавьте в него переменные

```
TESTPALM_OAUTH_TOKEN= # https://oauth.yandex-team.ru/authorize?response_type=token&client_id=6d967b191847496a8a7077e2e636142f
HITMAN_OAUTH_TOKEN= # https://oauth.yandex-team.ru/authorize?response_type=token&client_id=637ca17604cb4dfa90b262952c00b1e9
STARTREK_OAUTH_TOKEN= # https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b
CONFIG= # можно посмотреть в https://reactor.yandex-team.ru/browse/resolve?path=/maps/front/maps/sloth/example/config
ST_ISSUE= # номер задачи в которой будете отлаживаться
STAGE=CREATE_VERSION_AND_BOOK # стадия которую хотите запускать на npm start
TESTRUN_SIZE_LIMIT_MB=7
```

После того как все заполнено можете запускать `npm start`. Не забудьте поудалять брони/версии созданные в процессе отладки.
