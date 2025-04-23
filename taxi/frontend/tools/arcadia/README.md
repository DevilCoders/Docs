# Сборка образа

Сборка образа делается через multistage. 
1. Ставятся зависимости, делаются тесты и билдится проект от базового образа `node:<version>-slim`;
2. В базовый образ rtc (production | testing) копируется папка сбилженного проекта, а также необходимых конфигов.

## Как собирается?

Весь докерфайл разбит на мелкие части. Базовая часть в этой папке, а куски реализации того или иного метода лежат в каждом сервисе.

Таким образом, мы получаем почти лего-домик, где каждый может на любом шаге сделать (или даже отключить) необходимый для себя функционал.

Перед запуском команды `docker build` все части докерфайлов конкатинируются в единый файл. После чего финальный файл и скармливается команде как multi-stage сборка.

На выходе мы получаем оптимизированную сборку клиентского приложения без лишних зависимостей.

## Аргументы

Следующие переменные передаются в сборку и можно использовать через ARG:

* NODE_VERSION — версия nodejs из вашей папки package.json сервиса;

## Что остаётся решить?

1. Поменять базовый образ RTC на наш. Сейчас базовый образ весит ~~дофига~~ 6 Гб. [Ссылка на ресёрч](https://st.yandex-team.ru/TXIFM-275). Это позволит иметь результирующий образ во много раз меньший. Что ускорит и сборку, и деплой в няню и всё остальное.

## Как запускать тесты сборки локально?

Детальнее про запуск на писано в папке `__tests__`.

## Как запушить конкретную версию nodejs в taxi-frontend образ?

Локально:
```
NODE_VERSION=<major> npm run ci:nodejs:publish
NODE_VERSION=16 npm run ci:nodejs:publish
```

В ТимСити (TODO: ссылка на сборку).  
Если не хватает прав на пуш, нужно [запросить тут](https://idm.yandex-team.ru/user/v-pereskokov/roles#rf=1,rf-role=gTDhSxYa#docker/distribution_prefix/taxi-frontend%7C(fields:()),f-status=all,sort-by=-updated,rf-expanded=gTDhSxYa).

## Как запускать локально скрипт паблиша пакета

Нужно пробросить явно аргументы перед стартом скрипта.
```
NODEJS_BIT_PATH="" NPM_EMAIL="<login>@yandex-team.ru" NPM_USER="<login>" NPM_REGISTRY="https://npm.yandex-team.ru" NPM_PASS="<pass>"  npm run ci:packages:publish-login -- --packageName=hiring-i18n
NODEJS_BIT_PATH="" NPM_EMAIL="<login>@yandex-team.ru" NPM_USER="<login>" NPM_REGISTRY="https://npm.yandex-team.ru" NPM_PASS="<pass>"  npm run ci:packages:publish-default -- --packageName=hiring-i18n
```

Например:
```
NODEJS_BIT_PATH="" NPM_EMAIL="robot-yataxi-daniel@yandex-team.ru" NPM_USER="robot-yataxi-daniel" NPM_REGISTRY="https://npm.yandex-team.ru" NPM_PASS="AQAD-<pass>"  npm run ci:packages:publish-login -- --packageName=hiring-i18n
NODEJS_BIT_PATH="" NPM_EMAIL="robot-yataxi-daniel@yandex-team.ru" NPM_USER="robot-yataxi-daniel" NPM_REGISTRY="https://npm.yandex-team.ru" NPM_PASS="AQAD-<pass>"  npm run ci:packages:publish-default -- --packageName=hiring-i18n
```
