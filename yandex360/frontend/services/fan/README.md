# Fan (Рассылки, Рассылятор)

Client:
[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=yandex360/frontend/services/fan/client&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/fan/client)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=yandex360/frontend/services/fan/client&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/fan/client)

Server:
[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=yandex360/frontend/services/fan/server&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/fan/server)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=yandex360/frontend/services/fan/server&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/fan/server)

## TL;DR

Сервис, предоставляющий пользователям доменной почты (ПДД, Яндекс 360 для бизнеса, Коннект etc.) услуги массовой рассылки писем.
Призван ~~заработать нам кучу денег~~ усилить привлекательность b2b-предложения платной подписки, а также со временем в том числе заменить
существующий [внутренний сервис](http://sender.yandex-team.ru) с аналогичным функционалом.

Команда: https://abc.yandex-team.ru/services/fan

Wiki: https://wiki.yandex-team.ru/fan

Трекер: https://st.yandex-team.ru/FANFRONT

Прод: https://send.yandex.ru/ ([qloud](https://qloud-ext.yandex-team.ru/projects/mail/fan-front/production)) ([Deploy](https://yd.yandex-team.ru/stages/mail_fan_production))

QLOUD
Престейбл: https://prestable.fan.common.yandex.ru/ ([qloud](https://qloud-ext.yandex-team.ru/projects/mail/fan-front/prestable))
DEPLOY
Престейбл: https://fan-prestable.mail.yandex.ru/ ([Deploy](https://yd.yandex-team.ru/stages/mail_fan_prestable))

QLOUD
Тестинг: https://testing.fan.common.yandex.ru/ ([qloud](https://qloud-ext.yandex-team.ru/projects/mail/fan-front/testing))
DEPLOY
Тестинг: https://fan-testing.mail.yandex.ru/ ([Deploy](https://yd.yandex-team.ru/stages/mail_fan_testing))

Счётчик Метрики: 83987521

## Разработка

### Как запустить
- получить роль "Разработчик интерфейсов" в [ABC](https://abc.yandex-team.ru/services/fan)
- завести себе разработческую машину в QYP с пресетом `Mailfront` по [инструкции](https://github.yandex-team.ru/personal-services/frontend/tree/dev/tools/qyp)
- смонтировать аркадию на машинке по [инструкции](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)
- перейти в проект arcadia/yandex360/frontend/services/fan ([ссылка в аркадии](https://a.yandex-team.ru/arcadia/yandex360/frontend/services/fan))
- убедиться, что используется nodejs@14
```bash
$ node -v
v10.15 # если тут уже v14.*, переходим к следующему шагу
$ nvm install 14
$ nvm use 14
```
- установить зависимости
```bash
npm ci
```
- запустить dev-окружение
```bash
npm start
```
- насладиться интерфейсом через браузер по адресу, сформированному по принципу `https://<название_машинки>-arc.fan-dev.mail.yandex.ru`

Для разработки потребуется учётка в [тестовом Паспорте](https://passport-test.yandex.ru).
На момент написания доки рекомендуется использовать коммунальную разработческую учётку `yafantest` / `fantest`.

Если интерфейс почему-то не появился по нужному адресу:
- если это свежесозданная виртуалка, перезагрузить
- проверить, запущен ли nginx на виртуалке (`sudo service nginx status` => `sudo service nginx start`)
- перезапустить dev-окружение, используя debug-режим (`DEBUG=core:* npm start`)
- перезапустить dev-окружение, зачистив предварительно артефакты сборки (`git clean -fdx`)
- почитать логи nginx (`/var/log/nginx/fan/access.tskv`, `/var/log/nginx/fan/error.log`, `/var/log/nginx/error.log`)
- ...
- громко плакать и звать коллег на помощь

### Как зарелизить

- завести версию в Трекере ([тык](https://st.yandex-team.ru/FANFRONT))
- завести релизный тикет Трекере ([тык](https://st.yandex-team.ru/createTicket?queue=FANFRONT&summary=%D0%9F%D1%80%D0%BE%D1%82%D0%B5%D1%81%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D1%82%D1%8C%20%D0%B8%20%D0%B2%D1%8B%D0%BA%D0%B0%D1%82%D0%B8%D1%82%D1%8C%20%D1%80%D0%B5%D0%BB%D0%B8%D0%B7%20v%7B%7B%D0%BD%D0%BE%D0%BC%D0%B5%D1%80_%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D0%B8%7D%7D&assignee=marchart))
- разметить все таски, находящиеся в ветке `dev` и релизный тикет созданной версией через поле "Исправить в версиях"
- отвести от актуального `dev` ветку `rc-fan-{{version}}`
- в корне проекта выполнить команду `npm run package {{version_with_patch}} {{ticket}} `
- дождаться сборки ресурса, в тикет {{ticket}} придет отбика, что ресурс версии vX.YY.ZZ собран
- выкатить пакет в тестинг и на престейбл: в корне проекта выполнить `make put-testing` и `make put-prestable`
- зайти в деплой и дождаться, когда выкатиться новая версия на престейбле и тестинге ([тут смотреть](https://yd.yandex-team.ru/projects/mail_fan))
- сообщить тестированию, что можно приступать
- дождаться "ОК" от тестирования
- выкатить пакет на продакшн, по аналогии с престейблом и тестингом выполнив команду: `make put-production`
  скрипт даст ссылку на черновик в деплое, нужно посмотреть, что в нем нужные вам изменения и закоммитеть его
- влить релизную ветку в `dev`

### Как обновить конфиг проекта

Если вы что-то поменяли  в файлах ```fan/tools/fs/***```, то вам необходимо собрать новый ресурс с конфигом и обновить его в скриптах сборки
Что нужно делать:

- в корне проекта fan в консоли выполнить простую команду: `make mailfront-config`
- дождаться завершения команды, и найти в консоли ID ресурса (если вдруг закрыли консоль/выключился компьютер, то можете найти ID ресурса конфига вот на [этой страничке](https://sandbox.yandex-team.ru/resources?type=MAILFRONT_CONFIG))
- изменить версию ресурса в файлах: 1) `fan/tools/specs/front-app.j2` в строчке `{% set settings_resource = "sbr:RESOURCE_ID" %}`
  2) `fan/tools/ci/qloud-stand` в строчке `const SETTINGS_RESOURCE_ID = 3077816236;` (актуально для стендов в qloud)

## Эксплуатация

### Графики

Серверное:
- [Основная панель фронта QLOUD](https://yasm.yandex-team.ru/panel/fellonbit.fan-front)
- [Основная панель фронта DEPLOY](https://yasm.yandex-team.ru/panel/fellonbit._syfRKH)
- [Панель фронтового S3](https://yasm.yandex-team.ru/panel/pistch.fan-front_s3/)
- [Общая панель сервиса](https://yasm.yandex-team.ru/template/panel/fan_panel/)

Клиентские метрики:
- [RUM](https://rum.yandex-team.ru/projects/fan/)
- [Error booster](https://error.yandex-team.ru/projects/fan/)

### Логи

YT:
- [Nginx](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Fhome%2Flogfeller%2Flogs%2Fmail-fan-production-frontend-nginx-access-log)
- [Duffman Access](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Fhome%2Flogfeller%2Flogs%2Fmail-fan-production-frontend-duffman-access-log)
- [Duffman Http](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Fhome%2Flogfeller%2Flogs%2Fmail-fan-production-frontend-duffman-http-log)

Сlickhouse (mailch), пример запроса со всеми таблицами: [YQL](https://yql.yandex-team.ru/Operations/YYAHpZfFt-O5vCXs3LYfM5dktnsqMq2lpXqoa-4FlnA=)

[Logbroker](https://logbroker.yandex-team.ru/logbroker/accounts/mail-fan/production/frontend?page=browser&type=directory)

### Алерты

Проект в Juggler — `fan-front`.

- [Проверки](https://juggler.yandex-team.ru/aggregate_checks?project=fan-front)
- [Правила эскалации](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=61547d43d163680d54d408aa&project=fan-front)

## Не разработка

Пара полезных рецептов, связанных с фронтом (складывать в браузерную консоль для наибольшей эффективности):
- узнать текущую версию фронта
```javascript
JSON.parse(document.getElementById('config-environment').textContent).version
```
- проставить себе фича-флаги (нужен json, в примере форсированно включена фича `my-feature` и насильно выключена `not-my-feature`)
```javascript
document.cookie = 'yandex.fan.features={"my-feature": true, "not-my-feature": false}'
```
NB: Последовательные вызовы этой команды будут полностью перетирать предыдущие вызовы
