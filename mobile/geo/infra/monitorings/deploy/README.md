# Сервер для мобильных мониторингов Яндекс.Карт и Навигатора

## Общая схема работы
Мониторинги представляют из себя набор cron тасков, которые запускаются каждую минуту.
[.config/cron/mobile-crash-data.conf](./.config/cron/mobile-crash-data.conf)

Каждая cron таска обращается к shell скрипту, задача которого, вызвать соответствующий node скрипт. 
[tools/mobile-monitoring/](./tools/mobile-monitoring/)

**Задачи node скрипта:**
* Сходить в какое-нибудь API и забрать данные. Например, ClickHouse или AppMetrica.
* Каким-то образом агрегировать данные и сохранить их в файл.
* Например, get-mobile-crash-data.ts ходит в API AppMetrica получает уже агрегированную статистику по крэшам за 10 минут.

Скрипты выгружают результат работы в файлы, которые создаются в [tools/mobile-monitoring/init.sh](./tools/mobile-monitoring/init.sh).

Периодически Голован опрашивает каждый инстанс и забирает из него данные для мониторингов. <br />
Отдает данные в Голован, тулза из базового образа ubuntu. [.configs/deploy/README.md](./.configs/deploy/README.md) <br />
Для описания каждого из сигналов есть по скрипту, которые лежат в папке [.config/checks](./.config/checks). <br />
Эти скрипты отдают содержимое файлов, в которые cron таски сложили значения. <br />
https://github.yandex-team.ru/maps/docker-baseimages#roquefort

Как посмотреть данные в Головане: <br />
[../yasm/panels/README.md](../yasm/panels/README.md) <br />
[../yasm/alerts/README.md](../yasm/alerts/README.md) <br />

--- 

## Разработка
### Cкрипты
[tools/mobile-monitoring/README.md](./tools/mobile-monitoring/README.md)

### Docker
Для запуска Docker образа локально используем docker compose
* Собираем образ `docker compose build` 
* Разворачиваем образ локально `docker compose up`

Чтобы мониторинги заработали, нужно в файле [docker-compose.yml](./docker-compose.yml) проставить переменные окружения с паролями и токенами:
* `MOBILE_MONITORING_CLICKHOUSE_USER` и `MOBILE_MONITORING_CLICKHOUSE_PASSWORD` - пользователь и пароль, с которым скрипт будеи ходить в ClickHouse
* `HAMSTER_YT_TOKEN` - Токен для похода в YT https://oauth.yt.yandex.net/

--- 

## Деплой
* Поднимаем версию (registry.tag) в [.qtools.json](./.qtools.json)
* Переключаемся на node нужной версии `nvm use` Если напишет, что nvm не установлен, то ставим nvm. https://github.com/nvm-sh/nvm#install--update-script
* Устанавливаем зависимости `npm ci`
* Собираем докер образ `node_modules/.bin/qtools build`. Токен для переменной окружения QTOOLS_TOKEN можно взять здесь: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=4dd38b9acbb44ad8a7ece163ddf1c53a.
* Пушим докер образ в registry `node_modules/.bin/qtools push`
* Деплоим только что собранный образ в Deploy `node_modules/.bin/qtools deploy production`
* Следим за деплоем https://deploy.yandex-team.ru/stages/maps-mobile-infra_production

---

## Доступ в registry

Образ мониторингов основан на образе `ubuntu_xenial-node_10-monitorings`, который тянется из `registry.yandex.net`

Что бы получить доступ к `registry.yandex.net` нужно залогинется:
https://wiki.yandex-team.ru/qloud/docker-registry/#authorization
```
$ docker login -u $(whoami) registry.yandex.net
Password: <OAuth token body>
```
`<OAuth token body>` - токен по ссылке https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1
