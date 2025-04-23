[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=yandex360/frontend/services/mobile-api&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/mobile-api)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=yandex360/frontend/services/mobile-api&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/mobile-api)

# API почты для мобилок

## Разработка

Используй qyp (см. [инструкцию](../../tools/qyp))

```sh
cd ~/arcadia/yandex360/frontend
npm ci
cd services/mobile-api
npm ci
npm start dev # or corp or testing
```

Апи будет доступен по адресу `https://<qyp-name>.verstka-dev.mail.yandex.ru`.
Если аркадия подмонтирована не в `~/arcadia`, то `https://<qyp-name>-<arc-folder>.verstka-dev.mail.yandex.ru`.

После запуска можно проверить на методе без авторизации:
```sh
curl https://<qyp-name>.verstka-dev.mail.yandex.ru/api/mobile/v2/versions
```

## Методы

https://psf.s3.mds.yandex.net/mobile-api-docs/index.html

## CI

https://a.yandex-team.ru/projects/mail_frontend/ci/actions/launches?dir=yandex360%2Ffrontend&id=ci

## Новые ручки

Новые ручки добавляются в `methods/vX/`, где X - номер версии. См. реализацию файлов `index.js` и `router.js` в папках routes/v1 и `routes/v2` в качестве примеров. Также нужно зарегистрировать новый путь в `config/routes/mobileapi.js`.

## NginX

Боевые конфиги [тут](./tools/fs/etc/nginx/sites-available)

## Secrets

Секреты должны лежать в config/secrets.json.
В Y.Deploy подкладываются из [sec-01cp55j5wxzfkph5fmbx5bgc2c](https://yav.yandex-team.ru/secret/sec-01cp55j5wxzfkph5fmbx5bgc2c)

## Сборка и деплой

Считаем ветку `trunk` всегда готовой к выкатке.

Проект в Y.Deploy: https://yd.yandex-team.ru/projects/mail_mobapi

Релизы mobile-api [запускаются в интерфейсе New CI](https://a.yandex-team.ru/projects/mail_frontend/ci/releases/timeline?dir=yandex360%2Ffrontend&id=mobapi_release). Слева можно заметить список веток (`trunk` и последние релизные ветки) со статусом текущего релиза, если есть (например, может быть подсвечен `Waiting For Manual Trigger`). Тикет в стартреке заводится автоматически.

Чтобы запустить релиз, [в интерфейсе CI](https://a.yandex-team.ru/projects/mail_frontend/ci/releases/timeline?dir=yandex360%2Ffrontend&id=mobapi_release) нужно выбрать коммит и отвести от него релизную ветку (справа в бургере), после этого перейти в ветку и нажать `Run release`. Релизная ветка отводится c автоматическим инкрементом мажорной версии. Наблюдать за релизом можно в UI. Некоторые шаги требуют ручного подтверждения (например, нужен запуск для деплоя canary и production окружений). Если какие-то кубики в процессе выполнения "покраснели" в результате временной ошибки (можно понять по логам), их можно перезапустить в UI.

[Пример релизного флоу](https://a.yandex-team.ru/projects/mail_frontend/ci/releases/timeline?dir=yandex360%2Ffrontend&id=mobapi_release&version=14)

Чтобы докинуть фикс в релиз (фикс должен быть в транке), можно черри-пикнуть его прямо в UI кнопкой `Cherry pick` (кнопка доступна сверху справа, если находиться при этом в релизной ветке), и запустить новый флоу `Run and cancel others` (кнопка в бургере у пикнутого коммита). В результате будет запущен новый релиз с инкрементом минорной версии.

Флоу поделен на стадии (prepare / build / testing / etc), каждая стадия может начать выполняться только если в предыдущем релизе она завершилась (именно поэтому "and cancel others").

Приложение работает на [универасальном базовом образе](https://wiki.yandex-team.ru/pochta/sre/deploy/front/).


## Мониторинги

https://warden.z.yandex-team.ru/c/mail__mobile_api/monitoring

Панели, добавленные в `.config/panels` выкатываются каждый раз при релизе. Можно и вручную: `npm run yasm:update`.


## Тестинг

Можно `curl`ить или `postman`ить запросы в апи с заголовком `Authorization: OAuth TOKEN`. Токен можно получить так:

В тестовом паспорте:

```sh
./tools/test-oauth.sh # спросит логин/пароль пользователя
```

В продовом паспорте:

```sh
./tools/prod-oauth.sh # спросит логин/пароль пользователя
```
