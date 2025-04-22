# Скриншотные тесты на компоненты

## Необходимые npm зависимости

* [puppeteer](https://github.com/GoogleChrome/puppeteer) - обертка над хромом.
* [jest-puppeteer](https://github.com/smooth-code/jest-puppeteer) - для запуска puppeteer.
* [jest-puppeteer-react](https://github.com/hapag-lloyd/jest-puppeteer-react) - для комбинирования webpack и jest-puppeteer.
* [jest-image-snapshot](https://github.com/americanexpress/jest-image-snapshot) - матчер скриншотов.
* [expect-puppeteer](https://github.com/smooth-code/jest-puppeteer/blob/master/packages/expect-puppeteer/README.md) - библиотека ассертов для puppeteer.

Не считая webpack, jest, babel и т.д.

> Внимание! Каждая версия puppeteer совместима по API с конкретной версией chrome.
Версия chrome зашита в докер-образе в jest-puppeteer-react.
Это означает, что puppeteer и jest-puppeteer-react нужно обновлять аккуратно.

## Как это работает
1. **(nodejs)** `jest-puppeteer-react` поднимает `puppeteer`, устанавливает соединение с гридом, запрашивает нужное количество браузеров (по числу воркеров)
1. **(nodejs)** тесты компилятся вебпаком, каждый файл теста (`test suite`) получает отдельный бандл
1. **(nodejs)** бандлы загружаются в s3 в бакет `jest-puppeteer-react/<какой-то рандомный uid>`
1. **(nodejs)** в nodejs запускается настоящий `jest`, `puppeteer` коннектится к порту одного из запущенных в гриде chrome. Все тесты исполняются настоящим jest
1. **(nodejs)** когда дело доходит до `await render()`, puppeteer отправляет chrome `page.goto(https://vertis-screenshot-tests-static.s3.mds.yandex.net/jest-puppeteer-react/<uid>/index.html?test=<имя теста>&bundle=<бандл теста>)`
1. **(chrome)** chrome идет на эту страницу, там грузится собранный webpack-бандл
1. **(chrome)** теперь на этой странице еще раз исполняется тест, но только теперь там функция `render()` уже браузерная. Она исполняет и монтирует реакт-компонент на страницу
1. **(chrome->nodejs)** chrome теперь может ответить обратно puppeteer "я загрузил страницу"
1. **(nodejs)** puppeteer отправляет chrome "сделай скриншот"
1. **(chrome->nodejs)** chrome делает скриншот и отдает его puppeteer
1. **(nodejs)** теперь можно прочитать эталон с диска и сравнить со скриншотом, который пришел из puppeteer

## Область применения

Такие тесты дороже обычных юнит-тестов, поэтому все, что можно проверить без
использования реального браузера, надо проверить без него.
Основное применение jest-puppeteer-react - скриншотные тесты на компоненты,
в том числе для media queries.

## Ограничения

Пока что jest-puppeteer-react не поддерживает before, after, beforeEach, afterEach, моки и таймеры.

## Примеры использования

### Обычный тест
```js
import React from 'react';
import { render } from 'jest-puppeteer-react';
import takeScreenshot from '@realty-front/jest-utils/puppeteer/tests-helpers/take-screenshot';

import Button from '../Button';

describe('Button', () => {
    it('render button', async() => {
        // эта штука соберет компонент и запустит его в хроме
        await render(
            <Button
                theme='realty'
                size='l'
                view='yellow'
            >
                Жёлтая кнопка
            </Button>,
            { viewport: { width: 100, height: 100 } }
        );
    
        // эта штука работает так же, как снепшоты в jest
        // в первый запуск запишет эталонный скрин
        // при несовпадении полученного скрина с эталоном тест упадет
        // в режиме дебага сделает wait
        expect(await takeScreenshot()).toMatchImageSnapshot();
    });
});
```

### Тест с кликом

```js
import React from 'react';
import { render } from 'jest-puppeteer-react';
import takeScreenshot from '@realty-front/jest-utils/puppeteer/tests-helpers/take-screenshot';

import Button from '../Button';
import styles from '../styles.module.css';

describe('Button', () => {
    it('render alert after click', async() => {
        await render(
            <Button
                theme='realty'
                size='l'
                view='yellow'
                onClick={() => alert('Hello, world!')}
            >
                Жёлтая кнопка
            </Button>,
            { viewport: { width: 100, height: 100 } }
        );

        await page.click(`.${styles.wrap}`);
        expect(await takeScreenshot()).toMatchImageSnapshot();
    });
});
```

### Тест с ховером
```js
import React from 'react';
import { render } from 'jest-puppeteer-react';
import takeScreenshot from '@realty-front/jest-utils/puppeteer/tests-helpers/take-screenshot';

import Button from '../Button';
import Tooltip from '../Tooltip';

describe('Tooltip', () => {
    it('render tooltip after hover', async() => {
        await render(
            <Tooltip
                anchor={
                    <Button
                        className='my-button'
                        theme='realty'
                        size='l'
                        view='yellow'
                    >
                        Жёлтая кнопка
                    </Button>
                }
            >
                Hello, world!
            </Tooltip>,
            { viewport: { width: 100, height: 100 } }
        );

        await page.hover('.my-button');
        // ставим задержку 200ms, если нужно
        await page.waitFor(200);
        // передаем `keepCursor: true`, так как иначе во время
        // снимка курсор будет уведен в верхний левый угол экрана и тултип закроется.
        expect(await takeScreenshot({ keepCursor: true })).toMatchImageSnapshot();
    });
});
```

## Расширенное описание

Для тестов помимо задания имени можно добавить дополнительное описание, где более детально описать тест-кейс. Это описание попадет в allure-отчет и будет доступно тестировщикам.
```js
import { allure } from '@realty-front/jest-utils/puppeteer/tests-helpers/allure';

describe('Test', () => {
    it('Description', async() => {
        // ...

        allure.descriptionHtml(`
        <ol>
            <li>Юр. лицо</li>
            <li>Агент</li>
            <li>Спб</li>
        </ol>
        `);

        // ...
    });
});
```

## Работа с изображениями

По умолчанию любой сетевой запрос за картинкой будет возвращать серый пиксель. Если нужно протестировать вставку изображений разного размера в компонент можно воспользоваться двумя хелперами:

- generateImageUrl({ width, height, size }). Функция возвращает dataUri шахматного изображения размером width x height с размером квадрата size (параметр не обязательный).
- generateImageAliases({ width, height, size }). Функция возвращает набор алиасов для исходного изображения размером width x height. Так как это вернула бы аватарница.

Например:

```js
import React from 'react';
import { render } from 'jest-puppeteer-react';

import takeScreenshot from '@realty-front/jest-utils/puppeteer/tests-helpers/take-screenshot';
import { generateImageUrl, generateImageAliases } from '@realty-front/jest-utils/puppeteer/tests-helpers/image';

const Component = ({ image }) => <img src={image} alt="" />;

describe('Images', () => {
    it('image 200 x 100', async() => {
        const image = generateImageUrl({
            width: 200,
            height: 100
        });
    
        await render(<Component image={image} />, { viewport: { width: 400, height: 400 } });
    
        expect(await takeScreenshot()).toMatchImageSnapshot();
    });
    
    it('source image 300 x 150', async() => {
        const aliases = generateImageAliases({
            width: 300,
            height: 150
        });
        const image = aliases.appSnippetLarge;
    
        await render(<Component image={image} />, { viewport: { width: 400, height: 400 } });
    
        expect(await takeScreenshot()).toMatchImageSnapshot();    
    });

});
```

## Работа с Яндекс Картами

Если в тестируемом компоненте присутствуют Яндекс Карты, то можно дождаться отрисовки карты с помощью 2 методов:
1) `customPage.waitForYmapsPins` - основной, стабильный метод, нужно использовать, когда на карте есть пины
2) `customPage.waitForYmaps` - второстепенный, нестабильный метод, нужно использовать, когда на карте отсутствуют пины

```javascript
// index.browser.js

describe('ProfileCard', () => {
    it('correct draw features without offers in user geo', async() => {
        await render(<Component store={mocks.withoutOffersInUserRegion} />,
            optionsWide
        );

        await customPage.waitForYmapsPins();

        expect(await takeScreenshot()).toMatchImageSnapshot();
    })
})
```

## Работа с текущей датой и таймерами

В AppProvider необходимо передать параметр fakeTimers (под капотом используется либа [sinonjs/fake-timers](https://github.com/sinonjs/fake-timers)). После этого все функции работы с датой: Date, setTimeout, setInterval, ... - становятся замоканными и время останавливается.

Пример:

```js
const Component = (props) => (
    <AppProvider
        fakeTimers={{
            now: new Date('2020-06-02T03:00:00.111Z').getTime() // Начало отсчета времени
        }}
    >
        <MyComponent />
    </AppProvider>
);
```

Чтобы продвинуть время вперед, необходимо вызвать хелпер-функцию:

```js
await customPage.tick(1000);
```

При этом вызовутся все функции-обработчики зарегистированных таймеров, чьё время пришло.

## Моки для Gate

Есть возможность изолированно переопределять внутри каждого it гейты с помощью thunkExtraArgument. Для этого в экшене, который вызывает гейт необходимо использовать гейт-функцию не из realty-core, а из 3 аргумента reduxThunk.
Прокидывание 3 аргумента в проектах выглядит примерно [так](https://github.com/YandexClassifieds/realty-frontend/blob/fb2a04c12eda4dece65bb09964d6c90608814715/realty-www/view/react/libs/create-store.js#L28) [здесь](https://github.com/YandexClassifieds/realty-frontend/blob/fb2a04c12eda4dece65bb09964d6c90608814715/realty-www/entries/common/client.js#L42) и [здесь](https://github.com/YandexClassifieds/realty-frontend/blob/fb2a04c12eda4dece65bb09964d6c90608814715/realty-lk-www/view/lib/create-browser-app.js#L72).
Эта функциональность поддержана в `AppProvider` компоненте каждого проекта.

Чтобы написать стабильный тест, необходимо тестировать состояние запроса PENDING и SUCCESS/FAILED в разных тест-кейсах (читай в разных it секциях).

**Нестабильный** вариант имплементации Gate, поэтому **неправильный:**
```javascript
        const Gate = {
            get() {
                return new Promise((resolve) => {
                    setTimeout(() => {
                        resolve({ phones: [{ wholePhoneNumber: '+79992134916' }] });
                    }, 150);
                });
            },
        };
```

**Правильно:**
```javascript
import noop from 'lodash/noop';

        const Gate = {
            get() {
                // PENDING
                return new Promise(noop);
            },
        };
```
```javascript
        const Gate = {
            get() {
                // SUCCESS
                return Promise.resolve({ phones: [{ wholePhoneNumber: '+79992134916' }] });
            },
        };
```
```javascript
        const Gate = {
            get() {
                // FAILED
                return Promise.reject();
            },
        };
```

Пример: у нас есть экшн, который вызывает гейт, или несколько гейтов.

```javascript
// action.js

const getPhones = (arguments) => (dispatch, getState, { Gate }) => {
    return Gate.get('phones.get', arguments);
}
```

Пишем тест на компонент, где по клику на кнопку идет загрузка телефонов (дергается экшн сверху).

```javascript
// index.browser.js

const Component = ({ store, Gate }) => (
    <AppProvider initialState={store} Gate={Gate}>
        <PhonesContainer />
    </AppProvider>
);


describe('Телефоны', () => {
    it('Успешная загрузка одного телефона', async () => {
        const Gate = {
            get() {
                return Promise.resolve({ phones: [{ wholePhoneNumber: '+79992134916' }] });
            },
        };
    
        await render(<Component store={mocks.withOneOffer} Gate={Gate} />, getResolutions(SIZES.SHORT)[0]);
        
        // 1) начальное состояние - SUCCESS/INITIAL
        expect(await takeScreenshot()).toMatchImageSnapshot();
    
        // 2) нажали на кнопку, началось исполнение промиса
        await page.click(selectors.phoneButton);
    
        // 3) делаем скриншот обновленного состояния - SUCCESS
        expect(await takeScreenshot()).toMatchImageSnapshot();
    });
})
```

## Моки для экспериментов
в `jest-alias.js` проекта должно быть
```
'realty-core/view/common/libs/experiments': 'realty-core/view/mocks/experiments'
```

В провайдер компонента прокидываем `experiments` в формате `string[]`
```javascript
// index.browser.js

const Component = ({ store, Gate }) => (
    <AppProvider experiments={expNames}>
        <PhonesContainer />
    </AppProvider>
);
```

## Запуск локально

Мы используем `git-lfs`, чтобы хранить эталонные скриншоты.
Так они не раздувают индекс и репозитарий работает быстрее.
Устанавливается автоматически через `ansible`.

Необходимо:
* Запустить `/Applications/Docker.app` ([Если есть проблема с запуском на macOS](https://wiki.yandex-team.ru/users/diana-pure/dolgo-zapuskaetsja-docker-pod-macos/))
* Авторизоваться в [docker registry](https://wiki.yandex-team.ru/docker-registry/#authorization)
* Запустить `yarn test:screenshots`

> Если выполнить в корне репозитория, то тесты запустятся во всех проектах.

Под капотом обычный вызов `jest` - можно передавать нужные [ключи](https://jestjs.io/docs/en/cli). Например для запуска определенного теста:

```
yarn test:screenshots -t MyComponent
```

> Флаг `-t` очень долго отрабатывает, так как запускает все, но в процессе скипает лишнее, лучше запускать тест указывая путь до файла - `yarn test:screenshots view/components/Breadcrumbs/__tests__/index.browser.tsx`

# Удаленный дебаг тестов

[Selenoid](https://aerokube.com/selenoid), который используется для запуска браузеров в гриде позволяет удобно дебажить тесты

## Видео-дебаг
Во время записи тестов записывается видео, по которому можно отследить ход выполнения тестов - тут используется не headless-браузер, поэтому могут быть некоторые расхождения в рендеринге, но все равно часто помогает понять, что что-то идет не так

1. Запустить `yarn test:screenshots-video`
2. В логах после прохождения тестов появятся ссылки на записи браузерных сессий. Тут надо учитывать, что один браузер прокликивает несколько файлов с тестами - придется поискать нужный

Для CI можно добавить в нужный запуск env-переменную `VIDEO_DEBUG=1`

## VNC-дебаг
Во время запуска тестов открывается VNC-сессия, можно перейти по ссылке в логах и смотреть в реалтайме на браузер и управлять им. Тут также используется не headless-браузер, поэтому некоторые расхождения могут быть

1. Для удобства вставить `await jestPuppeteer.debug();` в нужном месте (`jestPuppeteer` это глобальный объект, который создает обвязка `jest-environment-puppeteer`)
2. Запустить `yarn test:screenshots-vnc-debug`
3. В логах появятся ссылки на VNC-сессий - можно перейти, прокликать нужные стили

## Локальный дебаг теста

Подготавливаем тест:
```js
import React from 'react';
import { render } from 'jest-puppeteer-react';
import takeScreenshot from '@realty-front/jest-utils/puppeteer/tests-helpers/take-screenshot';

import Button from '../Button';

describe('Button', () => {
    // Добавляем only, если тестов больше одного
    it.only('должен отрендерить жёлтую кнопку', async() => {
        await render(
            <Button
                theme='realty'
                size='l'
                view='yellow'
            >
                Жёлтая кнопка
            </Button>,
            { viewport: { width: 100, height: 100 } }
        );

        // Ставим debugger, если нужно. Обязательно после render и до takeScreenshot
        debugger;
        
        expect(await takeScreenshot()).toMatchImageSnapshot();
    });
});
```

В режиме отладки можно вести разработку компонента с live-reload.

Запускаем тест `yarn test:screenshots-debug Button`

## Как перезаписать эталоны

Как и со снепшотами - запустить с флагом `-u` (перезапишутся все эталоны проекта):
```
yarn test:screenshots -u
```

Перезапись конкретного эталона:
```
yarn test:screenshots view/components/Breadcrumbs/__tests__/index.browser.tsx -u
```

## Как перезаписать эталоны, используя результат запуска в CI

В кубике с упавшими тестами будет бейдж "Упавшие скриншоты", по клику на который откроется таска.

Затем с помощью make-команды [apply-screenshots-from-ci](../tools/make/screenshots.mk) (запускать в **корне проекта**) можно перезаписать все упавшие эталоны:

* либо используя ID таски (взять из URL, либо скопировать из заголовка на странице таски)
```
make apply-screenshots-from-ci SCREENSHOTS_TASK_ID=1234567890
```
* либо используя ссылку на архив (можно взять также на странице таски)
```
make apply-screenshots-from-ci SCREENSHOTS_ARCHIVE_URL=http://sandbox0000.search.yandex.net:12345/path/to/result_resources/failed_screenshots.tgz
```
