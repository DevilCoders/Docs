# Billing Admin

## Подготовка для первоначального запуска

### <a id="settings"></a> Настройка проекта

Выполняем [начальную настройку](https://a.yandex-team.ru/arc_vcs/market/front/monomarket/wiki/start.md).

Вкратце шаги которые нужно выполнить в инструкции:
- Нужно примонтировать аркадию, чтобы использовать `ya tool`
- Устанавливаем `yammy` глобально (`npm i -g @yandex-market/yammy`)
- Выполняем в корне проекта(мономаркета) `yarn run bootstrap` (если после запуска команды выполнение останавливается на `+++ npx --cache /var/...`, нужно убедиться что стоит версия `npm@6.14`)
- Переходим в директорию проекта `/lib/apps/billing-admin`

### Настройка проекта на логрусе

Заходим на любой логрус(logrus01ed.market.yandex.net, logrus01vd.market.yandex.net, logrus01hd.market.yandex.net, logrus02vd.market.yandex.net).

Например
```
ssh logrus01hd.market.yandex.net -A
```
- На логрусе выполняем команду `make_wc`
- Выбираем `monomarket`
- Выполняем шаги по настройке проекта описанные выше ([Настройки проекта](#settings))
- Переходим в директорию проекта `/lib/apps/billing-admin`
- Стартуем сервер на логрусе `yammy start me server`

Aдрес балансера: `https://{ваш_логин}.billing-admin.monomarket.logrus01hd.yandex.ru` (пример для логруса logrus01hd)

## Команды для запуска проекта

### При первом запуске локально
`yammy build me deep`

### Локальный запуск, через две консоли
`yammy run me local:client` - для запуска клиентской части

`yammy run me local:server` - можно запускать один раз для синхронизации серверной части (всё, что связано с resolvers, bcm, entities)

### Запуск сервера на логрусе
`yammy start me server` (статика будет загружаться с localhost, если настроить синхронизацию с локальным билдом)

### Чтобы работала синхронизация с логрусом
Нужно настроить деплой серверного бандла.

Один из способов – кладём в isomorphic файл .deploy.json примерно такого вида
```
{
    "root": "/home/{userName}/monomarket_{userName}/lib/apps/billing-admin",
    "host": "logrus01hd.market.yandex.net",
    "port": 22,
    "username": "{ваш_логин}",
    "privateKey": "/Users/${userName}/.ssh/id_rsa",
    "passphrase": "{пароль_от_ssh}"
}
```

Или настроить синхронизацию папки `./lib` с логрусом через rsync или другими способами.

### Чтобы не собирать лишний раз исходники локально
`export YAMMY_NO_AUTOBUILD=1`

### Инвалидировать кэш, если нужно заново собрать пакеты
`export YAMMY_INVALIDATE=1`

### Линтеры локально
```
yammy run me test:typescript

yammy run me test:eslint:fix

yammy run me test:jest
```

## Автотесты
завести конфиг .ginny.conf.js, вот здесь пример https://paste.yandex-team.ru/5081739

в .bashrc добавить export GINNY_USER_CONFIG_PATH="$HOME/.ginny.conf.js"

`yammy run me test:hermione`

## Доступы

чтобы иметь доступ к маркетным репозиториям (откуда угодно, логрус, локальный ноут) нужно быть в организации

https://github.yandex-team.ru/market

и в группе https://github.yandex-team.ru/orgs/market/teams/market-frontend/members


необходимо запросить для себя доступы до балансеров (если их нет и они вам нужны)

https://puncher.yandex-team.ru?create_destinations=billing-admin.market.yandex.ru&create_destinations=billing-admin.tst.market.yandex.ru&create_destinations=billing-admin.pre.market.yandex.ru&create_protocol=tcp&create_locations=office&create_locations=vpn&create_ports=80&create_ports=443

так же в IDM надо запросить роли для просмотра тарифов и сверок (что потребуется)

Маркет Тестинг - Тарифница - {ваш выбор}

Маркет Тестинг - Чекер - {ваш выбор}

Маркет - Тарифница - {ваш выбор}

Маркет - Чекер - {ваш выбор}


## Полезные ссылки

бункер - https://bunker.yandex-team.ru/market-billing-admin/tanker

танкер - https://tanker.yandex-team.ru/project/market-billing-admin?branch=master

abc - https://abc.yandex-team.ru/services/marketbillingadmin/

релизы - https://tsum.yandex-team.ru/pipe/projects/market-billing/delivery-dashboard/billing-admin-release

метрика - https://metrika.yandex.ru/dashboard?group=day&period=week&id=84212014

секреты - https://yav.yandex-team.ru/?tags=market-billing-admin

сервисы в няне - https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_market_billing_admin/

тестинг - https://billing-admin.tst.market.yandex.ru/

престейбл - https://billing-admin.pre.market.yandex.ru/

прод - https://billing-admin.market.yandex.ru/


# технологии

фронтовый бэкенд - nodejs - @yandex-market/stout (самописный фреймворк для ноды)

клиент - reactjs + redux + redux-observable

# где что лежит?

## фронтовый бэкенд:

/app, /configs, /shared

## клиент:

базовые скрипты и компоненты для сбоки - /isomorphic

основной код самой админки - /client

основная обёртка клиента - это контейнер /client/containers/Layout

все роуты описаны в /client/routes

все рутовые компоненты для каждой страницы приложения надо искать в /client/containers, например рутовый компонент для страницы с черновиками тарифов лежит в /client/containers/Tariifs/TariffDrafts/index.ts

В подобных рутовых компонентах прописано всё, что надо подключить для данного стейта (эпики, редьюсеры, апи), всё, что подключено в таком месте, доступно во всех его дочерних компонентах

в /client/components лежат компоненты, которые могут использоваться во всех местах приложения

## Всё, что связано со стором

экшены - /client/actions

эпики - /client/epics

редьюсеры - /сlient/reducers

селекторы - /client/selectors


## всё, что связано с запросами на бэк

/client/bcm - непосредственное описание ручек

/client/resolvers - описание резолверов, которые осуществляют связь между клиентом и нодой

/clients/api - описание апи, которые мы дёргаем через эпики

/clients/entities - описание всех сущностей, используемых в приложении

/clients/types - описание всех типов, используемых на клиенте
