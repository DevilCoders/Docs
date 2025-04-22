# sandbox-hugin

- Проект в [Deploy](https://deploy.yandex-team.ru/projects/sandbox-hugin).

## Разработка

1) Для не-linux окружений требуется подготовить контейнер с `atop`. Пример можно найти в директории `atop/` проекта.
2) Подготовить секреты – `cp .env.example .env`. `CLICKHOUSE_PASSWORD` следует взять в [секретнице](https://yav.yandex-team.ru/secret/sec-01dn2bvx4303h4h8azp3evfzh7), `SANDBOX_AUTH_TOKEN` можно исспользовать [собственный](https://sandbox.yandex-team.ru/oauth).
3) Запустить приложение:

```
$ npm i
$ npm build
$ npm run dev
```

4) Запустить фронтенд:

```
$ cd ./ui
$ npm i
$ npm build
$ npm run start
```

## Деплой

```
$ npm i
$ npm run build
$ npm run build-ui
$ npm run docker-publish
$ ya tool dctl release docker search-interfaces/sandbox-hugin --release-type stable --tag `node -p 'require("./package.json").version'`
$ open https://deploy.yandex-team.ru/stages/sandbox-hugin/deploy-tickets
# Закоммитить тикет и дождаться раскатки.
```
