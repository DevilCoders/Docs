# MDH
Репозиторий фронтенда MDH


## Статические проверки

`npm run tsc`

## Проверка кода линтером

`npm run lint`

## Проверка форматирования кода

`npm run code-format`

## Форматирование кода

`npm run prettier:format-all`

## Локальная разработка (настройка)

- Запросить в тестовом IDM права на MDH(dev) для пользователя в yandex-team с ролями Соавтор и Управляющий (чтобы работать с Конструктором)
- Добавить в /etс/hosts строку `127.0.0.1               local.mdh-test.yandex-team.ru`
- Запустить `dev/dev_cert`. Если сертификат протух, новый можно заказать на https://crt.yandex-team.ru/certificates, а после этого обновить dev-cert.sh
- С помощью `dev/nginx/create_cfg.sh` создать конфигурацию nginx и скопировать ее в его директорию конфигов. Где это, можно узнать с помощью `nginx -t`. На Mac это м.б. `/usr/local/etc/nginx/servers`.

## Локальная разработка

`npm run start`

Зайти https://local.mdh-test.yandex-team.ru/

## Сборка в CI

При любом пуше в master автоматически собирается, пушится и обновляется в https://deploy.yandex-team.ru/stages/mdh-test-stage/config/du-frontend/box-Box1

На комит проставляется тег, бег комитотега

![](https://jing.yandex-team.ru/files/enovikov11/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202021-08-20%20%D0%B2%2021.34.44.png)

## Локальная сборка докера, если нужна отдельная ветка

Залогиниться в docker:
```bash
docker login -u <login> registry.yandex.net
<token_body><Enter>
^D
```

`token_body` - Oauth токен получить по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1).

Подробнее [здесь](https://wiki.yandex-team.ru/qloud/docker-registry/#cli).

Далее выполнить

`npm run release`

И обновить https://deploy.yandex-team.ru/stages/mdh-test-stage/config/du-frontend/box-Box1 той версией, которую напишет скрипт

## Какие переменные окружения нужны в deploy

Для прода:
```
REACT_APP_ENV=production
REACT_APP_API_ROOT=https://api.mdh.yandex-team.ru/uiapi
REACT_APP_ISSUE_ROOT=https://st.yandex-team.ru
REACT_APP_METRIKA_ID=83615080
```

Для тестинга и веток:
```
REACT_APP_ENV=testing
REACT_APP_API_ROOT=https://api.mdh-test.yandex-team.ru/uiapi
REACT_APP_ISSUE_ROOT=https://st.test.yandex-team.ru
REACT_APP_METRIKA_ID=83615143
```
