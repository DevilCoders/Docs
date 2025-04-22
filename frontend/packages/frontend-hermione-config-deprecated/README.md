# Общий (deprecated) конфиг Hermione для frontend

**НЕ ИСПОЛЬЗУЙТЕ ЭТОТ ПАКЕТ! ИСПОЛЬЗУЙТЕ ПАКЕТ `frontend-hermione-config`!**

## Quickstart

Установить Hermione и этот пакет в проект:
```bash
npm install --save-dev hermione
npm install --save-dev @yandex-int/frontend-hermione-config-deprecated
```
Добавить конфигурацию hermione:
```bash
mkdir -p ./.config/hermione/ && cp ../../packages/frontend-hermione-config-deprecated/hermione.conf.js ./.config/hermione/hermione.conf.js
```

Тесты создаются в папке `tests/hermione/suites/` с расширением `.hermione.js`.

По умолчанию все тесты запускаются в десктопном хроме на linux.

### Для проектов, использующих kotik

В коде конфига добавить kotik-специфичную часть:
```js
const config = require('@yandex-int/frontend-hermione-config-deprecated/get-hermione-conf')(require('../../package.json').name);
const updateKotikConfig = require('@yandex-int/frontend-hermione-config-deprecated/kotik/init-hermione-config');

updateKotikConfig(config);

// ...

module.exports = config;
```

Добавить npm-команды для запуска тестов в package.json:
```json
{
  "scripts": {
    "hermione": "archon hermione --config .config/hermione/hermione.conf.js",
    "hermione:gui": "archon hermione gui --config .config/hermione/hermione.conf.js",

    "ci:hermione": "npm run build && npm run hermione"
  }
}
```

### Для проектов, использующих templar [deprecated]

Установить в проект `templar-runner`:
```bash
npm install --save-dev @yandex-int/templar-runner
```

Обновить конфиг плагина `templar-runner` в конфиге `hermione` проекта:
```js
const config = require('@yandex-int/frontend-hermione-config-deprecated/base.hermione.conf');
const updateTemplarRunnerConfig = require('@yandex-int/frontend-hermione-config-deprecated/templar/init-hermione-config.js');

updateTemplarRunnerConfig(config);

// ...

module.exports = config;
```

Добавить npm-команды для запуска тестов в package.json:
```json
{
  "scripts": {
    "hermione": "hermione --config ./.config/hermione/hermione.conf.js",
    "hermione:gui": "npm run hermione -- gui",

    "ci:hermione": "npm run build && npm run hermione -- --play --retry 4"
  }
}
```

### Добавить правила eslint
```bash
echo '{"extends": "../../node_modules/@yandex-int/frontend-hermione-config-deprecated/hermione.eslintrc.json"}' > tests/hermione/suites/.eslintrc
```

### Запуск тестов

Пример теста `tests/hermione/suites/morda.hermione.js`:
```js
describe('Морда Яндекса', function() {
    it('содержит в названии "Яндекс"', async function() {
        const {browser} = this;

        await browser.url("yandex.ru");
        const title = await browser.getTitle();

        assert.include(title, "Яндекс");
    });
});
```

Запуск тестов:
```bash
$ npm run hermione

> @yandex-int/stub@0.0.1 hermione /Users/slava-b/projects/customers/frontend/serp-73719/services/stub
> hermione --config ./.config/hermione/hermione.conf.js

✓ Морда Яндекса содержит в названии "Яндекс" [desktop-chrome:d0eaafd47ae61e9f9cbd5ad7b2763de6bef0fc24e4735eb22d9346965546f350] - 3025ms
Total: 1 Passed: 1 Failed: 0 Skipped: 0 Retries: 0
Your HTML report is here: file:///Users/slava-b/projects/customers/frontend/serp-73719/services/stub/__reports/__report-hermione:ci/index.html
```

### Для существующих проектов

Выполни все действия для новых проектов. Для переноса дампов и скриншотов смотри инструкцию в [tools в этом пакете](tools/README.MD)

## Возможности из коробки

### webdriver.io v4
Hermione основана на четвертой версии wdio: http://v4.webdriver.io/

### chai
В тестах предоставляется глобальная переменная `assert` из пакета chai: https://www.chaijs.com/

### html-reporter
Для построения отчетов используется плагин html-reporter: https://github.com/gemini-testing/html-reporter

Отчеты сохраняются в папку __reports/report-hermione:ci

### wdio-polyfill
Предоставляет полифиллы некоторых команд для браузеров: https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/wdio-polyfill

### gui-assistant
Расширяет команду gui, позволяя реиспользовать результаты прогона из sandbox: https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/gui-assistant

Опция --from принимает ссылку на задачу в sandbox:
```bash
npm run hermione:gui -- --from https://sandbox.yandex-team.ru/task/377202807
```
или на отчет:
```bash
npm run hermione:gui -- -f https://proxy.sandbox.yandex-team.ru/836174894/index.html
```
Не работает реиспользование по ссылке на PR:
```bash
npm run hermione:gui -- -f https://github.yandex-team.ru/search-interfaces/frontend/pull/962

...

Error: Нет завершенных запусков hermione для https://github.yandex-team.ru/search-interfaces/frontend/pull/962

...

server shutting down
```

### console-notifier
Выводит в консоль текст `FAQ: https://wiki.yandex-team.ru/search-interfaces/testing/hermione/#faq` в случае падения теста

### hermione-debug
Предоставляет доступ к браузерам в гриде по VNC, позволяет записывать видео, ретраить тесты до падения: https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/hermione-debug

```bash
npm run hermione -- --grep "имя теста" -b "linux-chrome" --debug --debug-vnc-before-test 1 --debug-pause-on-vnc 1
```

### json-reporter
Для построения json-отчетов о результате прогона тестов используется плагин json-reporter: https://github.com/gemini-testing/json-reporter. Включается только в CI. Результаты данных отчетов используются в [testcop](https://github.yandex-team.ru/search-interfaces/testcop) и [schetovod](https://github.yandex-team.ru/search-interfaces/schetovod)

Отчеты сохраняются в папку __reports/report-hermione:ci.json

### hermione-image-minifier
Для сжатия эталонных изображений без потери качества: https://github.com/gemini-testing/hermione-image-minifier

### hermione-muted-tests
Отключает заскипанные тесты во время запуска тестов: https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/hermione-muted-tests. При обращении к тесткопу плагин использует имя папки сервиса как идентификатор проекта.

### Конфигурация браузеров
Пакет содержит [конфигурацию браузеров](./get-browsers.js). Среди них есть десктопные браузеры в linux-окружении, эмуляция touch-устройств с их помощью и мобильные браузеры в эмуляторе android.

Желательно все новые конфигурации браузеров добавлять в этот пакет, а не в отдельные проекты.

Проект может изменить конфигурацию браузера при необходимости (например, изменить требуемое разрешение) в кастомном конфиге hermione.

Конфигурации браузеров именуются `ОС/эмулятор-браузера-девайс`. Например:
* `linux-chrome` - chrome, запущенный под linux
* `linux-chrome-ipad` - chrome, запущенный под linux, в режиме эмуляции ipad
* `appium-chrome-pad` - chrome, запущенный под [appium](http://appium.io/), в режиме эмуляции pad-устройства

### Запуск в trendbox
В [trendbox](https://wiki.yandex-team.ru/trendbox-ci/) запускается команда `ci:hermione`, ссылка на отчеты появляется в описании задачи.

## Планируемые возможности

### specs() в корне тестов

https://st.yandex-team.ru/SERP-81605

```js
specs({
    feature: 'Страницы профиля',
    experiment: 'Маленькие тумбы'
}, () => {
    it('Добавление услуги', async function() {
    });
});
```

Код hermione-тестов чуть более похож на .yml-файл. Из полей `category`, `feature`, `type`, `experiment` формируется имя suite.

### Очистка cookies и localStorage перед началом теста

https://st.yandex-team.ru/SERP-81606

В рамках одной selenium-сессии запускается несколько тестов. Эти тесты могут влиять друг на друга. Очистка cookies и localStorage поможет их изолировать.

### Загрузка тестовых ассетов

https://st.yandex-team.ru/SERP-81609

В тестах возникает необходимость добавить кастомный js или css. Например, отключить анимацию или спрятать окно, создаваемое сторонними модулями.

### Стаб картинок

https://st.yandex-team.ru/SERP-81610

Внешние по отношению к проекту картинки желательно стабать, как это делается в web4.

## Кастомизация

### Конфигурация hermione
Конфиг кладется в .config/hermione/hermione.conf.js. [Формат конфига](https://github.com/gemini-testing/hermione#hermioneconfjs).

### Команды

По-умолчанию в конфиге включён плагин `hermione-ya-commands` который содержит набор [общих команд](https://a.yandex-team.ru/arc_vcs/frontend/packages/hermione-ya-commands/README.md).

Кастомные команды проекта загружаются из папки `tests/hermione/commands`. Каждый файл экспортирует одну команду. В контексте команды `this` - это объект `browser`. Имя команды будет совпадать с именем файла.
```js
module.exports = function(selector, message) {
    return this
        .isVisible(selector)
        .then(isVisible => {
            if (Array.isArray(isVisible)) {
                throw new Error('Найдено более одного элемента. ' +
                    `Пожалуйста, используйте более конкретный селектор. Исходный селектор - ${selector}`);
            }
            assert.isTrue(isVisible, (message ? message + '. ' : '') + `Элемент с селектором ${selector} не виден!`);
        });
};
```

Использование:
```js
await browser.yaShouldBeVisible(PO.RegistrationForm.AddPhoneButton(), 'Кнопка добавления номера телефона не видна')
```

## Вопросы и ответы

### Почему в этом пакете нет templar-runner?

Предполагается, что проекты откажутся от templar и templar-runner в пользу kotik + archon-dev-server. Когда это произойдет, конфиг соответствующего плагина может попасть в этот пакет.
Сам пакет templar-runner тянет за собой templar и очень много зависимостей, поэтому он не включен в пакет.
