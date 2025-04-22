## Tacman

Прод: https://tacman.yandex-team.ru
Тестинг: https://testing.tacman.yandex-team.ru

Построен на основе `Create React App`.

**React + Typescript + CSS**

Сервис состоит только из фронтенда, который ходит в трекерное АПИ с кукой пользователя.
Вся статика хранится на S3 и проксируется через Awacs балансер.

#### Запуск проекта

1. Установить зависимости в корне монорепы-фронтенда. Без этого не будут работать линтеры и прекомитные проверки.

```bash
# Переходим в корень монорепозитория фронтенда https://a.yandex-team.ru/arc_vcs/frontend/
cd ../..

nvm use # как установть NVM https://github.com/nvm-sh/nvm#installing-and-updating
npm install --no-package-lock
```

2. Установить зависимости проекта
```bash

# В папке проекта https://a.yandex-team.ru/arc_vcs/frontend/services/tacman
npm install --no-package-lock

```

3. Локальная разработка
```bash
# 1. Получите токен для работы с Трекером
# https://wiki.yandex-team.ru/tracker/api/#avtorizacija
# export ST_API_TOKEN=<token>

# 1. Получите токен для работы с YT
# https://yt.yandex-team.ru/docs/description/common/auth
# export REACT_APP_YT_TOKEN=<token>

# Запустить dev режим
npm start

# если нужен тунель
npx @yandex-int/tunorok-cli 5000 --realm yandex-team
```

#### Релизный флоу
1. апнуть версию в `package.json`
1. cделаnm PR с изменениями
2. пройти ревью
3. написать комментарий в ревью-реквесте `/merge` для мержа
4. после мержа в `master` статика выкладывается на s3 в течении 15 минут (таску деплоя можно найти тут https://sandbox.yandex-team.ru/tasks?children=true&desc_re=Deploy%3A%20master&forPage=tasks&hidden=true&order=-updated&owner=FRONTEND&page=1&pageCapacity=20&type=TRENDBOX_CI_JOB_BETA&input_parameters=%7B%7D&output_parameters=%7B%7D)
5. 
    1. поменять версию в балансере для прода https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tacman2-awacs-balancer.yandex-team.ru/upstreams/list/tacman-prod/show
    2. поменять версию в балансере для тестинга https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tacman2-awacs-balancer.yandex-team.ru/upstreams/list/tacman-test/show
6. готово

#### Обновить конфиг
1. запустить команду `npm run update-tacman-config`
2. обновить сервис через стандартный релизный цикл


#### Шаблоны для datalens
https://datalens.yandex-team.ru/navigation/li2xn7w7r9v6d-tacman
