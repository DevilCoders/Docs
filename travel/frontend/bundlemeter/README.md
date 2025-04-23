# bundlemeter (beta)

[![npm version](https://badger.yandex-team.ru/npm/@yandex-data-ui/bundlemeter/version.svg)](https://npm.yandex-team.ru/release-dude)
[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=travel/frontend/bundlemeter&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/bundlemeter)
[![oko vulnerabilities](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=travel/frontend/bundlemeter&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/bundlemeter)

Этот инструмент открывает страницу в браузере, собирает информацию о размере js, css, img, font и отправляет ее в clickhouse.

## Где живет

-   Сборка в TeamCity - https://teamcity.yandex-team.ru/project/DataUI_YaTravel_YaTravelDevTools_Bundlemeter

## Install

`npm i --save-dev @yandex-data-ui/bundlemeter`

## Запуск

Нужно добавить в package.json скрипт, вызывающий команду:

```bash
bundlemeter --config ./config.js
```

Так же необходимо убедиться, что у вашей ноды проставлена переменная окружения `NODE_EXTRA_CA_CERTS`, содержащая путь до корневого сертификата (https://crls.yandex.net/YandexInternalRootCA.crt). Таким образом, команда может принять такой вид:

```bash
NODE_EXTRA_CA_CERTS=/usr/local/share/ca-certificates/Yandex/YandexInternalRootCA.crt bundlemeter --config ./config.js
```

`config.js` - это конфиг вида:

```ts
type config = {
    clickhouse?: {
        dbName: string;
        tableName: string;
        host: string;
        port: string;
        username: string;
        password: string;
        version: string;
        serviceName: string;
    };
    include: string | string[];
    exclude?: string | string[];
    args?: string[];
};
```

Пример содержимого файла с конфигом:

```ts
module.exports = {
    clickhouse: {
        uri: 'https://user:password@clikhouse-host:port',
        dbName: 'db_bundlemeter',
        tableName: 'travel',
        serviceName: 'travel',
        version: '0.0.0',
        host: 'clikhouse-host',
        port: 'port',
        username: 'user',
        password: 'qwerty',
    },
    include: './src/**/*.js',
};
```

## Тесты

В файле с тестом нужно вызвать глобальную функцию `cover`.
Первый аргумент - название страницы, второй - адрес страницы.
Пример:

```javascript
cover('index', 'https://travel.yandex.ru');
```

Страницы можно собирать и императивным путем, либо комбинировать.

## Дополнительные возможности

1. Перед началом замера страницы можно выполнить дополнительные действия, например, поставить куки или эмулировать платформу. Для этого существует третий аргумент функции `cover` - асинхронная функция, принимающая первым аргументом объект [page](https://github.com/GoogleChrome/puppeteer/blob/v1.17.0/docs/api.md#class-page). Пример:

```javascript
cover('index', 'https://travel.yandex.ru', async function (page) {
    await page.emulate({
        name: 'iPhone 4',
        userAgent:
            'Mozilla/5.0 (iPhone; CPU iPhone OS 7_1_2 like Mac OS X) AppleWebKit/537.51.2 (KHTML, like Gecko) Version/7.0 Mobile/11D257 Safari/9537.53',
        viewport: {
            width: 320,
            height: 480,
            deviceScaleFactor: 2,
            isMobile: true,
            hasTouch: true,
            isLandscape: false,
        },
    });
});
```

2. Если в конфиге не указать поле clickhouse, то результат работы отобразится в консоли.

## Известные проблемы

1. Для запуска в докере конфиг должен содержать

```javascript
{
    //...,
    args: ['--no-sandbox'];
}
```
