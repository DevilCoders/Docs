# Фронтенд регистрационной анкеты ПИ2

README.md каталогом выше обязателен к прочтению.
Для сборки проекта необходим NodeJS v10+ (ранее требовался 8).
Для разработки нужно запустить все докер-контейнеры в корневом каталоге проекта:

```
$ cd ../
$ ./restart
```

После этого можно запускать фронтовый дев-сервер:

```
$ yarn watch
```

Сервер работает по урлу https://localhost.yandex.ru:3000/

## Как собрать и выложить релиз — frontend

 1. Проверить что другие люди не собирают релиз анкеты и написать о своем желании в слак `#anketa`
 1. Замержить задачу (или задачи) в master и удалить ветки
 1. Переключить рабочую копию на текущий master
 1. Поправить файл `./build` в дериктории form — раскомментировать и указать значение для VERSION. Значение — это текущая дата, плюс номер сборки за этот день (смотреть в deploy какие уже были. Пример - `VERSION=2018-04-16_1`)
 1. В файле `./build` закомментировать строку `cd api; ...` (мы выкладываем frontend, для выкладки frontend не нужно собирать backend. Комментарий через #, а не //)
 1. Запустить `./build` — он соберет докерный образ (пример команды запуска: `VERSION=2018-05-25_1 ./build`)
 1. Выполнить команду которую выдал `./build` (Команда `docker push registry.yandex.net/partners/form_front:$VERSION"` в которой вместо `$VERSION` находится настоящая версия) — это зальет образ в общеяндексовый регистри
 1. Выложить образ в тестовое окружение deploy — https://deploy.yandex-team.ru/stages/form-test
 1. Проверить работу анкеты на ТС https://partner2-test.yandex.ru/form/
 1. Выложить образ в препрод окружение deploy — https://deploy.yandex-team.ru/stages/form-preprod
 1. Проверить работу анкеты на препроде https://partner2-preprod.yandex.ru/form/
 1. Если все ок, то выложить образ в прод окружение deploy - https://deploy.yandex-team.ru/stages/form-prod
 1. Отправить source maps в sentry (смотри как это сделать ниже)

# Загрузка Source Maps в Sentry

Фронтенд логирует ошибки и исключения в Sentry. Для читаемого трейса в Sentry нужно отгружать source map'ы исходников. Требуется одноразовая настройка.

## Установить `sentry-cli`
```
$ brew install getsentry/tools/sentry-cli
```

## Авторизоваться
выполнить `sentry-cli --url https://sentry.t.yandex-team.ru login`

создать токен с правами `project:read` и `project:releases`

смотри https://docs.sentry.io/cli/configuration/ если что-то идет не так

## Отправить Source Maps в Sentry
```
$ yarn run uploadSourceMaps
```

При отправке будет создан новый релиз, в качестве идентификатора которого будет использован commit id текущего HEAD.

## Локально перелогиниться
подобная процедура может потребоваться для тестирования:
1) в файле `form/blackbox/blackbox.json` захардкожен пользователь с которым мы работаем - для того что бы его сменить достаточно поменять login и uid-value

## Как удалить из базы тестовый логин 
после после заполнения анкеты тестовый пользователь добавляется в базу и его будет перекидывать либо в дашборд, либо во вторую часть анкеты, что бы вернуться на первую часть анкеты нужно:
1) зайти по ssh на dev-partner: `ssh dev-partner`
2) подключиться в базе к mysql на ТС:  `mysql_partner2 --server=ts`
3) выполнить следующие команды (можно единым куском копирнуть и запустить):
```
delete from form_data where id = 607369863;
delete from users_action_log where elem_id = 607369863;
delete from user_role where user_id = 607369863;
delete from context_on_site_campaign where owner_id = 607369863;
delete from owner_site where user_id = 607369863;
delete from site_action_log where user_id = 607369863;
delete from mail_notification where user_id = 607369863;
delete from user_adfox where user_id = 607369863;
delete from users where id = 607369863;
```