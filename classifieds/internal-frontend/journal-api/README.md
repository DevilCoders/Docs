# journal-api
API для сервисов: журнал Авто.ру / журнал Недвижимости 2.0.

## С чего начать разработку?
1. Установи зависимости:
    `npm ci`
2. Запусти dev-сервер. При запуске нужно указать env-переменную `JOURNAL_API_DOMAIN` для подключения к БД нужного сервиса:
`JOURNAL_API_DOMAIN=autoru` - Авто.ру, `JOURNAL_API_DOMAIN=realty` - Недвижимость.
  `JOURNAL_API_DOMAIN=realty npm run dev`
3. ...
4. PROFIT?

### Команды
* `JOURNAL_API_DOMAIN=realty npm run dev` запуск node в режиме дебага
* `JOURNAL_API_DOMAIN=realty npm start` запуск node (прод режим)
* `make start-db` запуск docker-образа с локальной базой для тестов
* `make stop-db` остановка docker-образа с локальной базой для тестов
* `JOURNAL_API_DOMAIN=realty npm run test:run` запуск тестов (требует запущенной локально базы)
* `JOURNAL_API_DOMAIN=realty npm run test:watch` запуск тестов в watch-режиме (требует запущенной локально базы)

### Сваггер
* [Сваггер](./docs/swagger.md)

## Миграции
Для работы с миграциями, используется консольная утилита [sequelize](https://github.com/sequelize/cli):

`npx sequelize-cli —-help`

Утилита позволяет работать с dev- и prod-базами. Настройки хранятся в `lib/database/config.js` в секциях `development` и `production`.
По-умолчанию, используются development-настройки.

### Работа с продовской базой
Перед тем, как подключиться к продовской базе, сходи в [секретницу](https://yav.yandex-team.ru/?tags=vsif,mysql), возьми пароль и замени его в соответствующей переменной в `.env` в корне проекта.

Теперь ты можешь подключиться к продовской базе нужного сервиса:

`NODE_ENV=production JOURNAL_API_DOMAIN=realty npx sequelize-cli db:migrate:status --env production`

Верни обратно пароль дев-базы❗

### Создание миграции
`npx sequelize-cli migration:generate --name add-new-fields`

После этого, в папке `lib/migrations` появится файл миграции с примерным именем: `20201028181445-add-new-fields.js`, в котором будет два метода `up` и `down`.

### Запуск миграции
Перед запуском миграций, желательно проверить их текущий статус:

`JOURNAL_API_DOMAIN=realty npx sequelize-cli db:migrate:status`

Для запуска всех не поднятых миграций, используй команду:

`JOURNAL_API_DOMAIN=realty npx sequelize-cli db:migrate`

### Откат миграций
Откат последней миграции:

`JOURNAL_API_DOMAIN=realty npx sequelize-cli db:migrate:undo`

Откат всех миграций

`JOURNAL_API_DOMAIN=realty npx sequelize-cli db:migrate:undo:all`

## Ссылки
* [deploy manifest](https://github.com/YandexClassifieds/services/blob/master/deploy/journal-api.yml)
* [Yandex Cloud с кластерами БД](https://yc.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-mysql)

Хосты Авто.ру (test):
* sas-4j53hhad1nkkb03u.db.yandex.net
* vla-p0xt41zgej8rf46l.db.yandex.net

Хосты Авто.ру (prod):
* sas-mv4u9dr3ey0bxfvc.db.yandex.net
* vla-jbr5arqqaqh60rog.db.yandex.net

Хосты Недвижимости (test):
* sas-2x6yk7yvrc14jetu.db.yandex.net
* vla-lk78q0447872tlwa.db.yandex.net

Хосты Недвижимости (prod):
* sas-jnciuyc7bkkzudot.db.yandex.net
* vla-w4olocgzulxyr92t.db.yandex.net

### Графики
* [Графана (приложение)](https://grafana.vertis.yandex-team.ru/d/ONI1NTsMz/vsif-api?orgId=1&var-datasource=Prometheus)
* [Соломон (БД)](https://solomon.yandex-team.ru/admin/projects/vertis-internal-frontend/dashboards)

