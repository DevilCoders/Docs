# Лего

- [Самое главное](#imp)
- [Что такое Лего?](#what)
- - [Файловая структура](#what-structure)
- - - [Контрибы](#what-contribs)
- - - [`canary`-версии](#what-canary)
- - - [Структура блока](#what-block)
- [Как собирать примеры?](#examples)
- - [i-bem](#examples-ibem)
- - [React](#examples-react)
- [Как писать тесты?](#tests)
- [А дальше что?](#flow)

<a name="imp"></a>
## Самое главное

`npx bem make {desktop,touch-{phone,pad}}.examples/link` Собрать все примеры блока `link`.

`npx bem make {desktop,touch-{phone,pad}}.tests/link` Собрать тестовые страницы блока `link`.

### Для notifier
`npm run build-notifier-examples` - Собрать все примеры колокольчика

`npx bem make desktop.examples/notifier` - Собрать все примеры колокольчика на BEM

`REACT_BLOCK=notifier webpack --config=configs/webpack/webpack.config --config-name=static-examples` - Собрать все примеры колокольчика на React

`build-notifier-tests` - Собрать все тесты колокольчика на BEM

`cd packages/lego-on-react && npm run bempack desktop.react-tests/notifier` - Собрать все тесты колокольчика на React

### Для lego-on-react
`cd packages/lego-on-react` - перейти в папку lor

`npm run bempack desktop.react-examples/link` Собрать все примеры блока `link` для `React`.

`REACT_BLOCK=link npm run react-hot-examples` То же самое, только горячая сборка.

`npm run bempack desktop.react-tests/link` Собрать тестовые страницы блока `link` для React.

```
npx hermione gui ./hermione/test-suites/common/link.hermione.js
npx hermione gui --config .config/hermione/hermione-react.conf.js ./hermione/test-suites/common/link.hermione.js
```
Запуск тестов на блок `link` для i-bem и React.

<a name="what"></a>
## Что такое Лего?
Лего — это библиотека блоков и общих элементов интерфейса Яндекса. Мы разрабатываем две версии библиотеки:
* `islands` на [i-bem](https://ru.bem.info/platform/i-bem/) c шаблонами [bemhtml](https://ru.bem.info/platform/bem-xjst/8/), [bh](https://github.com/bem/bh)
* `lego-on-react` на React

Ещё мы делаем версию библиотеки на TypeScript – `lego-components`.

![](https://jing.yandex-team.ru/files/smdenis/bilety__Yandeks_nashlos_839mlnrezultatov_2018-08-20_3_PM-06-56.png)

API блоков на разных стеках технологий не должен отличаться.

<a name="what-structure"></a>
### Файловая структура

Код библиотеки islands лежит в папках `projects/lego/packages/islands/*.blocks` – [уровнях переопределения](https://ru.bem.info/methodology/redefinition-levels/).

```
// Основной код библиотеки
packages/islands/common.blocks – уровень переопределения с общим для всех платформ кодом
packages/islands/desktop.blocks – десктопный код
packages/islands/deskpad.blocks – код для десктопов и планшетов
packages/islands/touch.blocks – общий код для тач-платформ
packages/islands/touch-pad.blocks – код для планшетов
packages/islands/touch-phone.blocks – код для мобильных

// Получается,
десктопы  = ['common', 'deskpad', 'desktop']
планшеты  = ['common', 'deskpad', 'touch', 'touch-pad']
мобильные = ['common', 'touch', 'touch-phone']

packages — скрипты и другие пакеты и блоки с независимым релизным циклом
hermione — hermione-тесты
```

<a name="what-contribs"></a>
#### Пакеты
```
packages
    _dist-generator
    _hermione-filenames
    _npm-scripts
    _palmsync-validate
    _prepare-publish
    _readme-md
    _specs-consistency
    ajax
    ci-helpers
    colors-inspector
    contribs-readme-generator
    counter
    detect-scripts
    doc-linter
    ensure-react-naming
    gap
    hedwig
    i-bem-react
    i-ua
    iframe-loader
    iver
    jest-bem-helpers
    lego-configs
    lego-dist-ts-generator
    pd-expanseur
    postcss-tone-vars
    rita-skeeter
    rpc
    selective
    selective-packages
    services
    slack-notifier-cli
    starter
    storybook-showcase
    tableau
    test-test
    tone-generator
    tools
    ts-docgen
    y-cookies
    yandex-font
    ...
    cookie-confirm
    i-bem
    islands
    islands-deprecated
    light-popup
    likes
    meccano
    messenger
    notifier
    pusher
    search-suggest
    suggest2
```

<a name="what-canary"></a>

#### `canary`-версии
Для тестирования изменений пакетов на сервисах использует механизм выпуска `canary`-версий.
Общие сведения о нем можно найти [здесь](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/services/hoolistener/insideCanary.md).

<a name="what-block"></a>
#### Структура блока (i-bem реализация)
```
*.blocks
    button2
        __элементы
        _модификаторы

        button2.md — документация на блок
        button2.meta.yml — общая информация о блоке

        button2.examples
            *.bemjson.js – декларация страницы с примерами на `i-bem`
            *.react.js – декларация страницы с примерами на `React`
            *.testpalm.yml — декларация для страниц с кейсами для ручного тестирования

        button2.tests — то же, что в .examples, только для авто-тестов

        button2.css – стили блока

        // i-bem
        button2.bemhtml.js – шаблон блока для шаблонизатора bemhtml.
        button2.bh.js – шаблон блока для шаблонизатора bh
        button2.js – клиентский код компонента
        button2.deps.js — зависимости блока
        button2.spec.js — юнит-тесты

        // react
        button2.react.js – код компонента
        button2.react.spec.js — юнит-тесты
```
[`bemhtml`](https://github.com/bem/bem-xjst/blob/master/docs/ru/2-quick-start.md) и `bh` превращают [данные в формате BEMJSON](https://ru.bem.info/platform/bemjson/) (как в `*.bemjson.js` файлах) в HTML.

<a name="examples"></a>
## Как собирать примеры?

<a name="examples-ibem"></a>
### i-bem:
`./node_modules/.bin/bem make <platform>.examples/<block>`
примеры `block` для платформы `platform` – `./node_modules/.bin/bem make desktop.examples/button2`.
Из деклараций страниц в `<block>.examples` в папке блока собираются HTML-странички в `/<platform>.examples/<block>`. Удобно запустить, например, `http-server` (`npm i -g http-server`) и смотреть их в браузере на `localhost:8080/desktop.examples/button2/`.

<a name="examples-react"></a>
### React:
`npm run react-hot-examples`
Поднимает `webpack-dev-server` с горячей сборкой на `http://127.0.0.1:8081`.

<a name="examples-typescript"></a>
### Lego-components:
См. документацию по TypeScript компонентам можно посмотреть тут:
[TypeScript lego-components](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/lego-components)

## Как писать тесты?
Мы пишем много разных тестов
* hermione — функциональное тестирование скриншотами. Используются одни и те же сценарии для i-bem и React.
Чтобы написать тест, нужно собрать тестовую страничку. Тестовые странички — это `bemjson.js` файлы в папке блока, например, `common.blocks/button2/button2.tests/hermione.bemjson.js`. Страницы для React генерируются из них же.
Тесты лежат в папке `hermione/test-suites`. Запуск `npx hermione gui ./path-to-test`.
* unit-тесты на jasmine и karma — поведенческие и JS API тесты i-bem-реализации компонент, сами тесты лежат рядом с кодом компонент в файле с расширением `spec.js` и все вместе по очереди запускаются на одной странице в браузерах в Selenium Grid через туннель, есть возможность запустить с локальным `PhantomJS`. Запуск `npx bem make specs desktop.specs/<блок>`.

Unit тесты на isladns состоят из двух видов тестов:
* tmpl-тесты — проверяют, что не сломались `bemhtml`/`bh`-шаблоны. Шаблонизируют `bemjson` и сверяют его с HTML-эталоном — `npm run tmpl-specs`
* unit-тесты на jest — поведенческое тестирование React-компонент, тесты построены и работают на `jsdom` без использования Selenium Grid. Запуск `npm run test-react`
* unit-тесты на внутренние пакеты — `lerna run test --parallel`

<a name="flow"></a>

## А дальше что?
- [Работа с репозиторием](https://github.yandex-team.ru/search-interfaces/frontend#%D0%B1%D1%8B%D1%81%D1%82%D1%80%D1%8B%D0%B9-%D1%81%D1%82%D0%B0%D1%80%D1%82)
- `commit-messages` оформляются по стандартам [`conventionalcommits`](https://www.conventionalcommits.org/en/v1.0.0-beta.3/).
Поддержаны следующие типы: `build`, `chore`, `ci`, `docs`, `feat`, `fix`, `perf`, `refactor`, `revert`, `style`, `test`.
Подробнее о типах можно прочесть в [the Angular convention](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#type).
- стартовать ревью командой `/start`
