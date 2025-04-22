# verdaccio-yandex-storage

Internal storage for Verdaccio.

## Run with docker

```bash
cd ~/infratest/packages/verdaccio-yandex-storage
curl 'https://proxy.sandbox.yandex-team.ru/1610367887/.npmusers' > config/.npmusers
docker-compose up
```

`verdaccio-yandex-storage` будет использоваться из текущего каталога, поэтому может потребоваться выполнить `npm run build`.

Необходимо, чтобы в окружении были доступны `AWS_ACCESS_KEY_ID` и `AWS_SECRET_ACCESS_KEY`.
[Как получить ключи от AWS](https://wiki.yandex-team.ru/search-interfaces/infra/report-renderer/kb/#i).
В свои dotfiles добавляйте переменные с `export` – иначе они не будут прокинуты.


## Fast Middleware

Middleware для отдачи 302 ответов можно использовать отдельно, она полностью отчуждаемая
При создании сервиса для неё требуются следующие переменные окружения (для метрик, базы и S3):
* METRICS_PORT
* DB_HOSTS
* DB_SSL
* DB_HOST
* DB_PORT
* DB_NAME
* DB_USER
* DB_PASSWORD
* AWS_ACCESS_KEY_ID
* AWS_SECRET_ACCESS_KEY

Для экспорта доступны 2 middleware:
* createFixTarsUrlsMiddleware - middleware для исправления url некоторых
запрашиваемых tar на формат verdaccio
* createFastProxyMiddleware - middleware отдачи и кеширования 302 ответов

## Smoke tests
Лежат в [infratest/deprecated/verdaccio-smoke-test](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/deprecated/verdaccio-smoke-test). Запускать можно после деплоя [на тестовый стенд](https://deploy.yandex-team.ru/stages/npm-test-stage).
