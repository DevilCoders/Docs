# islands-tools

[![Dependency Status](http://david.lego-dev.dev.yandex-team.ru/lego/islands-tools.svg)](http://david.lego-dev.dev.yandex-team.ru/lego/islands-tools) [![peerDependency Status](http://david.lego-dev.dev.yandex-team.ru/lego/islands-tools/peer-status.svg)](http://david.lego-dev.dev.yandex-team.ru/lego/islands-tools#info=peerDependencies) [![devDependency Status](http://david.lego-dev.dev.yandex-team.ru/lego/islands-tools/dev-status.svg)](http://david.lego-dev.dev.yandex-team.ru/lego/islands-tools#info=devDependencies)

Конфигурация `enb` для сборки библиотек `islands-*`.

-----

В ветке `master` находится версия, совместимая с библиотекой `islands` версии 4.x и выше.
Если вам нужна версия `islands-tools`, совместимая с более ранними версиями библиотек `islands-*`,
обратите внимание на ветку [support/2.x](https://github.yandex-team.ru/lego/islands-tools/tree/support/2.x).

## Установка

Установите себе в проект следующие пакеты:

Для сборки `islands-*` версий 2.x:

```sh
npm i --save-dev enb islands-tools bem-bl-xjst@1.x
```

Для сборки `islands-*` версий 3.x:

```sh
npm i --save-dev enb islands-tools bem-bl-xjst@2.x
```

## Настройка

В файле `.enb/make.js` подключите модуль `islands-tools` и вызовите
метод `configureProject` с требуемыми параметрами:

```javascript
module.exports = function(config) {
    config.includeConfig('islands-tools');

    var tools = config.module('islands-tools');

    tools.configureProject({
        // Cписок путей к зависимым библиотекам.
        // Блоки из этих библиотек попадают в сборку,
        // но примеры, тесты и документация для них
        // собираться не будет.
        libraries: [
            // такой способ следует использовать,
            // если библиотека содержит уровни вида
            // blocks-<platform>. В данный момент это
            // bem-bl и romochka
            {path: 'libs/bem-bl', levelPattern: 'blocks-*'},

            // такой способ следует использовать,
            // если библиотека содержит уровни вида
            // <platform>.blocks
            'libs/some-lib-1',
            'libs/some-lib-2',

        ],

        // Список уровней, необходимых для сборки библиотеки для каждой платформы.
        // Путь к уровню может быть абсолютным или относительным от корня проекта.
        // Используется вместо libraries для более тонкой настройки сборки.
        sourceLevels: {
            desktop: [
                '/path/to/level/common.blocks',
                '/path/to/level/desktop.blocks'
            ],
            'touch-phone': [
                '/path/to/level/common.blocks',
                '/path/to/level/touch.blocks',
                '/path/to/level/touch-phone.blocks'
            ],
            'touch-pad': [
                '/path/to/level/common.blocks',
                '/path/to/level/touch.blocks',
                '/path/to/level/touch-pad.blocks'
            ]
        },

        // Cписок путей к библиотекам, которые являются частью
        // проекта. В дополнение к блокам из настраиваемого проекта
        // в сборку также будут включены документация, примеры и тесты
        // из этих библиотек. Сами блоки из этих библиотек не попадут в
        // сборку, если библиотека не указана в `libraries`.
        bundledLibraries: [
            'libs/bundle-lib1',
            'libs/bundle-lib2'
        ],
        // собирать примеры для всех платформ.
        // если требуется сборка только для конкретных
        // платформ, можно указать их в виде массива, например:
        // examples: ['desktop', 'touch-phone']
        examples: true,

        // собирать документацию для всех платформ.
        // если требуется сборка только для конкретных
        // платформ, можно указать их в виде массива, например:
        // docs: ['desktop', 'touch-phone']
        docs: true,

        // опции для сборки документации
        docsOptions: {
            // список языковых суффиксов для документации
            // по умолчанию: ['ru']
            langs: ['ru'],

            // отключить сборку jsdoc (по умолчанию jsdoc собирается)
            noJSDoc: true
        },

        // собирать тестовые страницы hermione для всех платформ.
        // если требуется сборка только для конкретных
        // платформ, можно указать их в виде массива, например:
        // test: ['desktop']
        tests: true,

        // запускать юнит-тесты для всех платформ.
        // если требуется запуск только для конкретных
        // платформ, можно указать их в виде массива, например:
        // test: ['desktop']
        specs: true,

        // запускать тесты на шаблоны для всех платформ.
        // если требуется запуск только для конкретных
        // платформ, можно указать их в виде массива, например:
        // test: ['desktop']
        tmplSpecs: true,

        // опции для тестов на шаблоны
        tmplSpecsOptions: {
            // собирать bemhtml-шаблоны
            bemhtml: true,

            // собирать bh-шаблоны
            bh: true,

            // хранить js-параметры блоков в аттрибуте data-bem.
            // (по умолчанию используется onclick). Для версий
            // 3.x дожен быть установлен в true, для 2.x - в false.
            useDataBemInBh: true
        },

        // Определяет возможность создания инлайновых примеров из md-файлов.
        inlineExamples: true,

        // Возможность сборки бандлов
        bundles: true,

        // Отключить сборку css для ie6/7 (По умолчанию включена).
        legacyIE: false
    });

};

```

## Сборка библиотеки

1. Сборка примеров:

   ```sh
   enb make examples
   ```

   Собранные примеры будут в папках вида `<platform>.examples/<block>`

2. Сборка документации:

   ```sh
   enb make docs
   ```

   Собранная документация будет в папках вида `<platform>.docs/<block>`.
   Команда также запустит сборку примеров.

3. Сборка тестовых страниц для `hermione`-тестов:

   ```sh
   enb make tests
   ```

   Собранные страницы будут в папках вида `<platform>.tests/<block>`

4. Запуск юнит-тестов

   ```sh
   enb make specs
   ```

   Если требуется отладка:

   ```sh
   KARMA_DEBUG=1 enb make specs
   ```

5. Запуск тестов на шаблоны

   ```sh
   enb make tmpl-specs
   ```

   Если требуется сохранить получаемый в процессе работы HTML:

   ```sh
   TMPL_SPECS_SAVE_HTML=1 enb make tmpl-specs
   ```

6. Точечная сборка примеров/страниц/тестов/документации:

   ```sh
   enb make sets <путь>
   ```

7. Сборка бандлов

   Сборка всех бандлов для всех платформ:
   ```sh
   enb make bundles
   ```

   Сборка для конкретной платформы:
   ```sh
   enb make bundles <платформа>.bundles/*
   ```

   Сборка конкретного бандла:
   ```sh
   enb make bundles <платформа>.bundles/<имя-бандла>
   ```

## Запуск unit-тестов
Собрать и запустить тесты можно командой:
   ```sh
   npm test
   ```

Тесты запускаются в `selenium grid` при помощи библиотеки `karma`.

### Запуск в другом гриде
Адрес selenium сервера по умолчанию `sg.yandex-team.ru`. Его можно изменить переменными окружения:
  * KARMA_WD_HOST
  * KARMA_WD_BB_HOST
Где BB - короткое имя браузера в верхнем регистре (IPHONE, FIREFOX, CHROME, OPERA12, IE8, IE9, IE10).

`KARMA_WD_HOST` задает адрес сервера для выполнения всех тестов. `KARMA_WD_BB_HOST` позволяет поменять его для выполнения тестов в заданном браузере. Например, команда

   ```sh
   KARMA_WD_IE8_HOST=myhub.yandex.net npm test
   ```

запустит тесты для `Internet Explorer 8` на сервере `myhub.yandex.net`, тесты для остальных браузеров будут проходить на хосте по умолчанию - `sg.yandex-team.ru`.

Аналогично можно изменять порт сервера с помощью переменных `KARMA_WD_PORT` и `KARMA_WD_BB_PORT` (`BB` - имя браузера).

### Локальный запуск тестов
Для того, чтобы запустить тесты локально необходимо:
- установить karma-лаунчер
- передать путь к лаунчеру в переменной среды окружения `KARMA_CUSTOM_PLUGINS`
- указать браузер в переменной среды окружения `KARMA_BROWSERS`
- установить значение переменной среды окружения `KARMA_NO_TUNNEL` в `1`, `true`, `yes` или `on`

Например:
```sh
$ npm install -g karma-phantomjs-launcher
$ npm install karma-firefox-launcher
$ KARMA_NO_TUNNEL=1 KARMA_CUSTOM_PLUGINS=/usr/local/lib/node_modules/karma-phantomjs-launcher,`pwd`/node_modules/karma-firefox-launcher KARMA_BROWSERS=PhantomJS,Firefox npm run specs
```
Последняя команда выполнит тесты в PhantomJS и Firefox, не поднимая туннеля.

Еще можно так:
```sh
$ npm install -g karma-phantomjs-launcher
$ NODE_PATH=`npm root -g` KARMA_NO_TUNNEL=1 KARMA_CUSTOM_PLUGINS=karma-phantomjs-launcher KARMA_BROWSERS=PhantomJS npm run specs
```

Для удобства использования в наши библиотеки добавлен скрипт `specs-local`. Тесты будут запущены локально в `PhantomJS`, `karma-phantomjs-launcher` предварительно должен быть установлен глобально.
```js
$ npm install -g karma-phantomjs-launcher
$ npm run specs-local
```

При желании можно прописать custom launchers глобально:
```sh
$ echo 'KARMA_CUSTOM_PLUGINS=`npm root -g`/karma-firefox-launcher' >> ~/.bash_profile
$ source ~/.bash_profile
$ KARMA_NO_TUNNEL=1 KARMA_BROWSERS=Firefox npm run specs
```

### Запуск тестов локально в любом браузере
Можно запустить карму в режиме debug, при этом поднимется karma-server и будет висеть, пока кто-нибудь его не остановит.
```js
$ KARMA_DEBUG=1 npm run specs
...
INFO [karma]: Karma v0.12.31 server started at http://localhost:9876/
```
Если указанную ссылку (`http://localhost:9876/`) вставить в адресную строку любого браузера, то тесты запустятся.


### Список браузеров
Ограничить список браузеров, в которых будут запускаться тесты, можно двумя способами:
  * С помощью переменной среды окружения `KARMA_BROWSERS`

  ```sh
  KARMA_BROWSERS=firefox,chrome,ie8 npm test
  ```

  * Передав опцию `supportedBrowsers` при вызове базового конфига.

  Например, можно указать, что тесты для определенного уровня (`touch-phone`) могут гоняться только в мобильных браузерах:

  ```js
  var path = require('path'),
      baseConf = require(path.join('islands-tools', 'karma.conf.js'));

  module.exports = function(karma) {
      baseConf(karma, {
          supportedBrowsers: ['iphone']
      });
      // ...
  };
  ```

**Замечание**: если заданы и `supportedBrowsers` и `KARMA_BROWSERS`, то используется их пересечение. Т.е. если `KARMA_BROWSERS=firefox,chrome,iphone`, а `supportedBrowsers = ['iphone']`, то тесты запустятся только в `iphone`.

### Report-файлы

Если установлена переменная среды окружения `TEAMCITY_VERSION`, то `karma` использует `teamcity-reporter`, иначе `dot-reporter`.

## Проверка кода на опечатки
При установке модуля, в корень проекта копируются конфиг и словарь для [yaspeller](https://github.com/hcodes/yaspeller). Сам `yaspeller` прописан в `peerDependencies`, поэтому устанавливать его отдельно нет необходимости. В конфиге настроены расширения файлов, которые нужно проверять: md, js, css, bemhtml. В словарь нужно добавлять слова, которые `yaspeller` считает опечатками (их нет в базе Яндекс.Спеллер), но на самом деле таковыми не являются и должны оставаться в тексте как есть.

### Проверка на опечатки всех файлов блоков

```sh
yaspeller *.blocks
```

### Проверка конкретного файла

```sh
yaspeller [путь]
```

### Пополнение словаря
Для формирования форм слова удобно пользоваться тулзой [generate_paradigm_for_yaspeller](https://github.yandex-team.ru/invntrm/generate_paradigm_for_yaspeller)

Словарь: [.yaspellerrc](https://github.yandex-team.ru/lego/islands-tools/blob/master/common/.yaspellerrc#L24)

Слова отсортированы по алфавиту. Для поддержания сортировки можно пользоваться встроенной в текстовый редактор сортировкой (vim: `/dictionary` ⏎ `$vi[` ⏎ `:'<,'>!sort` ⏎, sublime: `выделить массив dictionary`, `⌘⇪P`, `sort` ⏎)
