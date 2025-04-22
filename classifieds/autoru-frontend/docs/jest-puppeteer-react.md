# Тесты на компоненты с jest-puppeteer-react

Верстку отдельного компонента можно протестировать с помощью jest-puppeteer-react.
* компонент собирается webpack'ом
* в headless-chrome под управлением puppeteer можно отрендерить компонент и делать с ним все что угодно
* можно сделать скриншот и сравнить с эталонным с помощью jest-image-snapshot (если скриншоты не совпадают, плагин сам построит дифф)
* тесты запускаются в гриде хедлесс-браузеров, но для отладки можно запускать локально с отключенным headless-режиме

# Подготовка
* настроить Git LFS, он будет нужен для хранения скриншотов вне основного индекса - [документация по настройке](git-lfs.md)
* установить [Docker for Mac](https://docs.docker.com/docker-for-mac/) и запустить. Для запуска тестов Docker должен быть в состоянии `Docker is running`. Если Docker зависает в `Docker is starting` - помогает [вот этот совет](https://github.com/docker/for-mac/issues/2420#issuecomment-439819670)
* [авторизоваться](https://wiki.yandex-team.ru/docker-registry/#authorization) в регистри. Докер-образ с puppeteer лежит в [яндексовом регистри](https://wiki.yandex-team.ru/vertis-admin/registry/), который требует авторизацию.

# Область применения

Такие тесты дороже обычных юнит-тестов, поэтому все, что можно проверить без использования реального браузера, надо проверить без него.
Основное применение jest-puppeteer-react - скриншотные тесты на компоненты, в том числе для media queries. Помни, скриншотным тестом ты тестируешь css, а не js.

Пока что jest-puppeteer-react не поддерживает describe, beforeEach, afterEach и моки.

# Примеры

```
const React = require('react');
const { render } = require('@vertis/jest-puppeteer-react');

const SalesItemPaidOffer = require('./SalesItemPaidOffer');

it('должен правильно отрендерить иконку платного оффера', async() => {
    const offer = {
        services: [
            { service: 'all_sale_activate' },
        ],
    };

    // эта штука соберет компонент и запустит его в хроме
    const page = await render(
        <SalesItemPaidOffer offer={ offer }/>
    );
    const screenshot = await page.screenshot();

    // эта штука работает так же, как снепшоты в jest
    // в первый запуск запишет эталонный скрин
    // при несовпадении полученного скрина с эталоном тест упадет
    expect(screenshot).toMatchImageSnapshot();
});
```

Можно задать вьюпорт, можно найти на странице нужный элемент и что-то с ним поделать (тут например наводим на элемент, ждем пока появится поп-ап и проверяем скриншот).

```
it('должен правильно отрендерить тултип про изменение цены', async() => {
    const offer = {
        hasPhoneRedirect: false,
        service_prices: [
            { service: 'all_sale_color', name: 'Выделение цветом' },
        ],
    };
    const page = await render(
        <SalesChart offer={ offer } data={ data }/>,
        { viewport: { width: 1220, height: 700 } }
    );

    // ховер на нужный элемент
    await page.hover('.SalesChart__iconDigit');

    //ждем пока появится поп-ап
    await page.waitForXPath('//div[contains(text(),"Изменена цена")]');

    const screenshot = await page.screenshot();
    expect(screenshot).toMatchImageSnapshot();
});
```

# Запуск тестов

```
npm run test:jest-screenshots
```

На коммит и пуш эти тесты не запускаются, но при желании можно запускать руками. Запускаются в тимсити на пулл-реквест.
Коммитить тесты надо вместе со скриншотами!

Запуск одиночного теста:

```
npm run test:jest-screenshots -- filename
```

# Удаленный дебаг тестов

[Selenoid](https://aerokube.com/selenoid), который используется для запуска браузеров в гриде позволяет удобно дебажить тесты

## Видео-дебаг
Во время записи тестов записывается видео, по которому можно отследить ход выполнения тестов - тут используется не headless-браузер, поэтому могут быть некоторые расхождения в рендеринге, но все равно часто помогает понять, что что-то идет не так

1. Запустить `npm run test:jest-screenshots-video`
2. В логах после прохождения тестов появятся ссылки на записи браузерных сессий. Тут надо учитывать, что один браузер прокликивает несколько файлов с тестами - придется поискать нужный

Для CI можно добавить в нужный запуск env-переменную `VIDEO_DEBUG=1`

## VNC-дебаг
Во время запуска тестов открывается VNC-сессия, можно перейти по ссылке в логах и смотреть в реалтайме на браузер и управлять им. Тут также используется не headless-браузер, поэтому некоторые расхождения могут быть

1. Для удобства вставить `await jestPuppeteer.debug();` в нужном месте (jestPuppeteer это глобальный объект, который создает обвязка jest-environment-puppeteer)
2. Запустить `npm run test:jest-screenshots-debug`
3. В логах появятся ссылки на VNC-сессий - можно перейти, прокликать нужные стили

## Локальный дебаг теста

1. В самом файле теста:
   - Поставить `it.only` если в файле тестов больше, чем 1 и нужно запустить один конкретный.
   - Вставить `await jestPuppeteer.debug();` в нужном месте (jestPuppeteer это глобальный объект, который создает обвязка jest-environment-puppeteer)
   - Третьим параметром в тест отправить таймаут, например `it.only('...', async() = {}, 10005000)`.

   *Пример теста, готового к дебагу:*
    ```
    it.only('должен выделить первый элемент по ховеру', async() => {
        const page = await render(
            <Context>
                <Provider store={ store }>
                    <CardGroupOtherComplectations
                        pageParams={ pageParamsMock }
                        groupID={ groupID }
                        groupSize={ offersCount }
                    />
                </Provider>
            </Context >,
            { viewport: { width: 1000, height: 1000 } }
        );

        await page.hover('.CardGroupOtherComplectationsItem');

        await page.waitForSelector('.Link_hovered');

        await jestPuppeteer.debug();

        const screenshot = await page.screenshot(); // когда дело до скриншота дойдет, браузер закроется

        expect(screenshot).toMatchImageSnapshot();
    });
    ```
1. Запустить `npm run test:jest-screenshots-local`

Для запуска нужен установленный Chromium (поставляется вместе с puppeteer-ом)

# ЛАЙФХАКИ!

- если в компоненте есть модал, оберни в `auto-core/react/components/islands/Modal/ModalTest`
- если в тесте надо замокать дату, не пиши MockDate в коде теста, оберни компонент в `mocks/components/DateMock.js`
