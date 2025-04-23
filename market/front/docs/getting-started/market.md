# Проект market

## Структура проекта

- `./src` — общий код, используемый всеми платформами и проектами
- `./market/platform.desktop` — Десктопная версия Яндекс.Маркета
- `./market/platform.touch` — Тачевая версия Яндекс.Маркета
- `./market/src` — общий код, используемый всеми платформами

**Цель** — максимально выносить код в `./src` и переиспользовать.

## Разворачивание проекта

На logrus'ах:

`make_wc`

Локально:

```bash
git clone git@github.yandex-team.ru:market/market.git market && cd market

# Разворачиваем Десктоп
cd platform.desktop && npm run configure && npm run bootstrap

# Разворачиваем Тач
cd platform.touch && npm run configure && npm run bootstrap
```

## Сборка и запуск

Запуск сервера: `cd platform.(desktop|touch) && npm run start`

Запуск сервера в debug-режиме: `cd patform.(desktop|touch) && npm run start:debug`

Запуск сборки: `cd platform.(desktop|touch) && npm run webpack`

Запуск сборки в watch-режиме: `cd platform.(desktop|touch) && npm run webpack:watch`

## Dev-стенды

- `https://%username%.desktop.market.logrus02vd.yandex.ru` — стенд Десктопа
- `https://%username%.touch.market.logrus02vd.yandex.ru` — стенд Тача
- `https://%username%.api.market.logrus02vd.yandex.ru` — стенд Фапи

## Линтеры

Линтеры, которые уже успели вынести в корень проекта.
Остальные продолжают жить в платформенных директориях.

- `npm run test:eslint:desktop` – проверка кодстайла Десктопа
- `npm run test:eslint:touch` – проверка кодстайла Тача
- `npm run test:eslint:src` – проверка кодстайла `src`-кода

- `npm run test:jest` – проверка юнит-тестов `src`-кода
- `npm run test:jest:updatesnapshot` – обновляет снепшоты юнит-тестов `src`-кода

- `npm run test:flow:coverage` – проверка flow coverage `src`-кода
- `npm run test:jest:coverage` – проверка юнит-тест coverage `src`-кода

## Линтеры в пулл-реквестах

Запускаются на каждое создание пулл-реквеста/добавления коммита в пулл-реквест.

Актуальный список линтеров в `sandbox-ci.json`.

## Библиотеки

[Stout](https://github.yandex-team.ru/market/monomarket/tree/master/lib/lib/stout).

[Mandrel](https://github.yandex-team.ru/market/monomarket/tree/master/lib/lib/mandrel).

[Apiary](https://github.yandex-team.ru/market/monomarket/tree/master/lib/lib/apiary/docs).

## Router

[Susanin](https://github.com/nodules/susanin).

Конфиг находится в `src/route/config/index.(desktop|touch).js`.

Для оптимизации матчинга самые "популярные" страницы следует располагать в начале списка.

Особенности использования:
```js
routes = [{
    name: 'Index',      // имя страницы, которая будет обрабатывать запрос
    pattern: '/',
    data: {
        method: 'GET',      // используется для матчинга запроса по HTTP-методу
        pageData: {         // необязательный атрибут. Передаётся в свойство data инстанцированной страницы
            authOnly: true,                 // включить проверку авторизации пользователя
            disallowedForRobots: true, // если true, то роут попадет в robots.txt в Disallowed
            addReqIdChain: true,            // добавлять в ответ страницы цепочку reqId
                                            // (нужно в ручках, которые меняют стейт приложения и историю)
            timeout: 15000,                 // если нужно задать особый таймаут для страницы
                                            // (или отдельного метода в случае JsonApiPage)
        }
    }
}];
```

## Логирование

Для логирования используется [logger](https://github.yandex-team.ru/market/monomarket/tree/master/lib/lib/error).

## Работа с ошибками

[BaseError](https://github.yandex-team.ru/market/monomarket/tree/master/lib/lib/error).

В приложении основной класс может быть расширен новыми кодами ошибок на уровне страниц, виджетов и ресурсов.

Пример использования:
```js
import BaseError from '@yandex-market/error';

class AnyError extends BaseError {}
```

## Ресурсы

Технически - функция обертка для похода до бэкенда.
Подробнее тут - [Resource](https://github.yandex-team.ru/market/marketfront/tree/master/src/utils/resource).

## Дата и время

[DayJs](https://github.com/iamkun/dayjs). :calendar:

## Операции с деньгами

[market-money-helpers](https://github.yandex-team.ru/market/market-money-helpers). :moneybag:

И хелперы распиханные по сущностям и компонентам, например - [src/entity/price](https://a.yandex-team.ru/arc_vcs/market/front/apps/marketfront/src/entities/price/utils.js)

## Валидация

Валидацию, например в хэндлерах, делаем с помощью [validator](https://github.yandex-team.ru/market/validator), в основе которого лежит [Validate.js](http://validatejs.org/).
Поддерживаемые ограничения можно найти в репозитории.

Пример работы:
```js
import {inspect} from '@yandex-market/validator';

const CONSTRAINTS = {
    userAddressId: {
        presence: true,
        string: true,
    },
}

const handle = async (ctx, params) => {
    const errors = inspect(params, CONSTRAINTS);

    if (errors) {
        return {
            error: new AnyError(Object.values(errors).join('; ')),
        };
    }

    return anyResolver(ctx, params);
}
```
