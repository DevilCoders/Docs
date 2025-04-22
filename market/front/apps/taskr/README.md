# taskr

http://pvl4xz4kjvzsvrqj.sas.yp-c.yandex.net/queues/

## Использование

-   [Интерфейс](./docs/ui.md)
-   [Работа с очередями](./docs/queues.md)

[![taskr](docs/taskr.png)](https://excalidraw.com/#json=5661000774713344,W_HZyEIRXjNzow7LbUXECg)

Очереди и планирование задач реализованы поверх [redis](https://github.com/redis/redis) с помощью [bull](https://github.com/OptimalBits/bull).

## Разработка

### Quick start

Установить зависимости:

```sh
npm install
```

Настроить локальный `.env` в корне:

-   Получить `YNDX_YT_TOKEN` через https://oauth.yt.yandex.net/
-   Получить `AWS_ACCESS_KEY_ID` и `AWS_SECRET_ACCESS_KEY` (см. https://wiki.yandex-team.ru/mds/s3-api/authorization/#upravlenieaccesskeys)
    > Также возможно потребуется запросить "Writer" права для MDS Маркета (или бакета marketpartner): https://idm.yandex-team.ru/system/s3-mds/roles#f-status=all,f-role=s3-mds,sort-by=-updated

#### Запуск с помощью докера

```sh
docker build --rm -t taskr .
docker run --rm --env-file .env -p 80:80 --name taskr taskr
```

#### Запуск без докера

> Необходимо в таком случае иметь поднятный `redis-server` с дефолтным доступом по `6379`

```sh
npm run start:server
```

### Deploy

Необходимо [запросить права](https://idm.yandex-team.ru/#rf-role=36178702#docker/distribution/market%7Cpartner%7Ctaskr/contributor(fields:()),rf-expanded=36178702,rf=1) на публикацию образов в докер-репозитории.

С помощью данной команды будет собран и опубликован образ под новую версию:

```
npm version <minor | patch | ...>

git push
```

Затем достаточно обновить версию образа в Яндекс.Деплое: https://deploy.yandex-team.ru/projects/taskr

Полезные ссылки:

-   подробнее про Yandex.Deploy: https://wiki.yandex-team.ru/users/kornilovyv/yadeploystepbystep/
