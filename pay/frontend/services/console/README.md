# Yandex Pay Admin

## Быстрый старт
### Подготовка
1. Установить [Hivemind](https://github.com/DarthSim/hivemind) или [Overmind](https://github.com/DarthSim/overmind)
1. Скачать [dev-сертификат](https://github.yandex-team.ru/Billing/trust-frontend/blob/master/docs/start.md#dev-сертификат)
1. Подготовить локальную dev-середу\
   `cd tools/local && . prepare-dev.sh`
1. Установить [tvmtool](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#iznpm)\
   `npm install -g tvmtool-bin --registry=http://npm.yandex-team.ru/`


## Структура проекта
- `_config` — скрипты для сборки статики и локальной разработки
- `server` — Фронтбэк Yandex Pay Admin (Duffman-сервер)
- `client` — Клиент Yandex Pay Admin
- `tools` — Скрипты для CI/CD


## Локальная разработка
1. Установить все зависимости (См. Устрановка зависимостей) — `npm run local:deps`
2. Запустить проекты:
 - `hivemind` — будет использовать test.pay.yandex.ru для PayAPI
 - `MOCK_API=true hivemind` — будет использовать моки для PayAPI
 - `cd ./client && MOCK_SERVER=true npm run start` — будет запущен только клиент и замокан Duffman server

После этого, будут доступны:
- Страница Регистрации [https://pay-admin.local.yandex.ru:4000/registration/](https://pay-admin.local.yandex.ru:4000/admin/registration/)
- Примеры UI элементов [https://pay-admin.local.yandex.ru:4000/ui/](https://pay-admin.local.yandex.ru:4000/admin/ui/)

_Разработка требует залогина в тетовом Паспорте._

### Установка зависимостей
Все зависимоти устанавливаются по след. правилам:
1. Если зависимость нужна в коде - ставим в packages.json пакета
2. Для пакетов в папке packges лучше устанавливать зависимости в peerDependencies
3. Во всех остальных случаях ставим в корневой packages.json


## Тестовый стенд
Развернут в Yandex.Deploy [https://deploy.yandex-team.ru/stages/yandexpay-admin-front-testing](https://deploy.yandex-team.ru/stages/yandexpay-admin-front-testing) \
Доступен по адресу [https://test.pay.yandex.ru/admin](https://test.pay.yandex.ru/admin)


## Деплой

_Пока делается вручную_

**1. Собираем и загружаем Docker-образ**
1. `git checkoput master && git pull origin master` — переходим в свежий мастер
1. `DOCKER_TAG=0.X.Y make local-build` — собираем и выгружаем Docker-образ
1. `git tag v0.X.Y && git push --tags` — помечаем релиз тэгом

**2. Выкатываем его в Yandex.Deploy**
1. Заходим в box — [ссылка](https://deploy.yandex-team.ru/stages/yandexpay-admin-front-testing/config/du-front/box-front)
2. Правим **Docker image** тэг на `0.X.Y`
