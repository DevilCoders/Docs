# `front-agency-cabinet` 🇷🇺
Фронтенд агентского кабинета для заведения рекламных кампаний в Геосервисах.

## Общая информация для разработки
Сервис живет в кулауде за общеяндексовым l7-балансером по пути `/geoadv/agency/`.

production:
https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/knoss_fast/upstreams/list/geoadv/show/

testing:
https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/knoss_fast_testing/upstreams/list/geoadv/show/

Роутинг идет через балансеры:

production:
https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/geoadv_agency_cabinet_production/show/

testing:
https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/geoadv_agency_cabinet_testing/show/

Для консистентности при разработке на локальной машине все пути тоже начинаются с `/geoadv/agency/`. Например, корневая страница на локалхосте открывается по урлу `https://geoadv.maps.dev.yandex.ru:8080/geoadv/agency/`.

### Настройка окружения

1. Следующие шаги можно сделать за одну команду `npm run setup:all`;

   1.1 `cd maps/front/services/agency-cabinet/` - переключаемся в папку с агентским кабинетом и устанавливаем локальные npm-зависимости.

   1.2 `npm run setup:install-ya` - скрипт, который поставит консольный питонячий клиент для яндексовой секретницы. _DISCLAIMER_: этот скрипт для Node.js-домохозяек. Если вы постоянно используете `python` и `pip` на вашей машине, то посмотрите в этот скрипт глазами. Возможно, он поставит вам что-нибудь не туда, где вы это привыкли видеть.

   1.3 `npm run setup:install-secrets` - скрипт, который установит в `~/.bashrc` и `~/.bash_profile` переменные окружения с секретами для паспорта, s3 и т.п.

   1.4 `npm run setup:install-dev-cert` - скрипт, который скачает из секретницы сертификаты для домена `geoadv.maps.dev.yandex.ru`, который мы используем как алиас для `localhost`, чтобы работала авторизация на домене `.yandex.ru`.

   1.5 `npm run setup:add-local-host` - скрипт, который пропишет алиас `127.0.0.1 geoadv.maps.dev.yandex.ru` в `/etc/hosts`.

   1.6 После этого надо добавить в системное хранилище сертификатов сертификат из папки `./.ssl/ssl.crt` и сделать его доверенным. Это сертификат на домен `geoadv.maps.dev.yandex.{{tld}}`, который мы только что скачали командой `npm run setup:install-dev-cert`. Это нужно, чтобы браузер доверял ответам от нашего сервера на локалхосте. [Инструкция по добавлению.](../docs/DEV_CERTIFICATES.md)

2. Установите необходимую версию NodeJS командой `nvm use`;

3. Установите `npm` зависимости `npm install`;

4. Чтобы запустить дев и поднять локальный nodejs-сервер, `npm run dev`.

### Как добавить нового пользователя

Добавление глобальной роли (аккаунт менеджер, ассессор и супер пользователь) внутри агенсткого кабинета:
1. Привязать почту к стаффовому аккаунту (желательно начинающуюся на yndx-...): https://wiki.yandex-team.ru/eva/search/staffprivateloginconnect/ .

Почта привязывается к стаффу для безопасности (ограничения: доступа только для сотрудников Яндекса и автоматический отзыв прав у уволившихся сотрудников) потому что глобальная роль дает доступ по всем агенствам и всем заказам.

2. Попросить кого-нибудь у кого есть роль суперпользователя добавить вас сообщив ему желаемую роль и вашу привязанную к стаффу почту. Добавить роль можно на странице:

production:
https://yandex.ru/geoadv/agency/global-permissions

testing:
https://l7test.yandex.ru/geoadv/agency/global-permissions

Добавление в dash (для выдачи фич конкретным пользователям):
1. получить idm роль "менеджер в кабинете рекламодателя"
   [IDM Prod](https://nda.ya.ru/t/sQP-1EtD3iXsc5)
   [IDM Test](https://nda.ya.ru/t/NHtjbhPc3ihZZa)
2. сделаать аккаунтом или выше (см. выше как);
3. в [Dash](https://yandex.ru/business/dash) / [Dash Test](https://l7test.yandex.ru/business/dash) выдать этому персонажу роль AgencyCabinetAccountManager
4. выдать этому персонажу роль RWSecurityDashboard

### [UI Packages DEMO](https://l7test.yandex.ru/business/ui/)

### Версионирование и деплой
Для создания нового релиза надо получить последний trunk `arc checkout trunk && arc pull` и выполнить команду `npm run rc:create`.
При этом поднимется минорная версия, отведется релизная ветка, задеплоится тестинг и создастся тиккет на тестирования релиза.
Эту команду можно выполнить самостоятельно по шагам:
1. `npm run rc:version minor`
2. `npm run rc:ticket`

Для того чтобы скрипты сработали корректно надо установить переменные окружения [`QTOOLS_TOKEN`](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=4dd38b9acbb44ad8a7ece163ddf1c53a), [`STARTREK_OAUTH_TOKEN`](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b) и [`ABC_OAUTH_TOKEN`](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=23db397a10ae4fbcb1a7ab5896dc00f6).

После выкатки тестинга нужно перевести все задачи в релизном тикете в "Можно тестировать". Это можно сделать командой `npm run rc:ticket-status-change <ISSUE_ID> readyForTest`, где ISSUE_ID - ключ тикета в Трекере.

При стабилизации релизной ветки, фиксы лучше всего коммитить в `trunk`, а потом добавлять коммит в релизную ветку. Для этого надо взять последний `trunk` `arc checkout trunk && arc pull`, перейти в релизную ветку `npm run rc:checkout <версия релиза>` и черрипикнуть в нее нужный коммит `arc cherry-pick <хэш коммита>`. Хэш коммита можно достать на страничке слитого пулл-реквеста в аркадии.

Если по каким-то причинам смержить в транк нельзя, можно завести пулл реквест с фиксом сразу на релизную ветку:
```
arc pr create --to releases/maps-front/agency-cabinet/<версия релиза>
```

Для релиза продакшена надо выполнить команду `npm run deploy:production`. Эта команда раскатит образ приложения в продакшн. При этом образ должен был быть собран и опубликован в docker-regestry при релизе тестинга.

После релиза продакшена изменения из релизной ветки надо слить в `trunk`:
```
npm run rc:merge
```
А в релизном тикете закрыть связанные задачи: `npm run rc:ticket-status-change <ISSUE_ID> closed`

### Поднятие тестового стенда

При создании PR trendbox триггерит в CI нужные скрипты и делает все сам автоматически!

Наименование стейджа `STAGE_ID` формируется пакетом `@yandex-int/maps-stand-tools`.

Stage'ы тестовых стендов в Y.Deploy:
- базовый Y.Deploy проект: https://deploy.yandex-team.ru/projects/maps-front-stands
- проект отделього стенда: `https://deploy.yandex-team.ru/projects/maps-front-stands_<STAGE_ID>`

Балансировщик для тестовых стендов:
https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/geoadv_agency_cabinet_dev_stands/show/

URI стендов формируются вида: `https://<STAGE_ID>.stands.maps.yandex.ru/geoadv/agency/`


### Запуск автотестов

1. Необходимо поднять стенд и получить его URI
2. Выполннить команду `STAND=<URI> npm run test:func`
