# Как запустить АТ и Кадавр

Содержание:

- [Словарь](#словарь)
- [Как развернуть окружение для запуска автотестов](#как-развернуть-окружение-для-запуска-автотестов)
- [Запуск](#запуск)
- [Как фильтровать тест кейсы](#как-фильтровать-тест-кейсы)
    - [Как фильтровать запуск автотестов с помощью переменных окружения](#как-фильтровать-запуск-автотестов-с-помощью-переменных-окружения)
    - [Как фильтровать запуск автотестов с помощью ginny.config.js](#как-фильтровать-запуск-автотестов-с-помощью-ginny.config.js)
- [Kadavr](#kadavr)
    - [Как запустить тесты с кадавром на тестинге](#как-запустить-тесты-с-кадавром-на-тестинге)
    - [Как запустить тесты с кадавром на логрусе](#как-запустить-тесты-с-кадавром-на-логрусе)
    - [Вносим правки в моки кадавра](#вносим-правки-в-моки-кадавра)

## Словарь

**Автотесты** - в Яндексе под автотестами принято называть интеграционные тесты ([selenium](https://www.selenium.dev/)).

**Selenium** - инструмент для автоматизации работы браузера ([wiki](https://wiki.yandex-team.ru/Market/Verstka/SeleniumCookBook/))

**Hermione** - тест раннер для интеграционных тестов, разработанный в Яндексе. ([github](https://github.com/gemini-testing/hermione))

**Gemini** - утилита для реегрессионого тестирования скриншотами разработанная в Яндексе. ([github](https://github.com/gemini-testing/gemini))

**Ginny** - Фреймворк для автоматического тестирования, разработанный в Яндекс.Маркете ([github](https://github.yandex-team.ru/market/ginny))

**Allure** - репортер для тестов, рисует отчеты. Разработан в Яндексе. ([github](https://github.com/allure-framework/allure2))

**Kadavr** - утилита разработанная в Яндекс.Маркете для моков http запросов исходящих из node.js приложений. ([github]())

**Page Object** - это шаблон проектирования, который широко используется в автоматизированном тестировании и позволяет разделять логику выполнения тестов от их реализации. Page Object инкапсулирует в себе логику для работы со сложным компонентом. ([подробнее](http://internetka.in.ua/selenium-page-object/))

**Селектор** – правило, по которому определяется расположение элемента на странице.

## Как развернуть окружение для запуска автотестов

0. Склонировать и собрать [partnernode](https://github.yandex-team.ru/market/partnernode/)
    ```bash
    cd папка-в-которой-хотите-хранить-исходники-ПИ
    git clone git@github.yandex-team.ru:market/partnernode.git
    cd partnernode
    make
    ```

1. Установить браузер [Chromium v74](https://github.com/macchrome/chromium/releases) (а под Windows - брать версию 78)

    В дополнение:
    - [Как быстро взять chromium нужной версии](https://wiki.yandex-team.ru/browser/dev/howto/kakbystrovzjatchromiumnuzhnojjversii/)
    - [MacOS](https://github.com/macchrome/chromium/releases/tag/v74.0.3690.0-r628207-macOS)
    - [win64](https://github.com/macchrome/chromium/releases/tag/v78.0.3866.0-r681261-Win64)
    - [Инсталлер для винды](https://disk.yandex.ru/d/2_pFAzdL5LrXIQ)

2. Установить Java JDK 8

    1. Установить [jdk-8u181-macosx-x64.dmg](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) или скачать macos версию с [Яндекс.Диска](https://disk.yandex.ru/d/m-5sf-b8khYI1A)
    2. Если у вас Mac, то установить Xcode Tools

    ```
    xcode-select --install
    xcode-select -p # /Library/Developer/CommandLineTools
    ```

    <details><summary>Если у вас Mojave (10.14)</summary>Зайти на <a href="https://developer.apple.com/download/more/">оф сайт</a> и скачать и установить <code>Command line Tools (macOs 10.14)</code></details>
    <details><summary>Если у вас Windows с WSL</summary>В WSL Ubuntu установить <code>sudo apt install openjdk-8-jdk</code></details>

3. Сохранить этот файл как `~/.ginny.conf.js`
    ```js
    // ~/.ginny.conf.js
    module.exports = {
        /**
         * URL стенда, на котором будут прогоняться АТ.
         *
         * логрус - https://gafarov.partner.market.node.logrus01vd.yandex.ru/
         * БТ/FSLB - https://partner.market.fslb.yandex.ru/
         * prestable - https://partner-prestable.market.fslb.yandex.ru/
         *
         * Поле сейчас закомментировано потому, что
         * оно ломает задание стенда через npm run at и AT_BASE_URL.
         */
        //baseUrl: 'https://partner.market.fslb.yandex.ru/',

        sessionsPerBrowser: 1,

        // чтобы запускать тесты без локального селениума, можно запустить их в гриде, раскомментировав строчку ниже
        // gridUrl: 'http://selenium:selenium@sg.yandex-team.ru:4444/wd/hub',

        hermione: {
            // опционально можно несколько раз перезапускать тест
            retry: 1,
            // таймаут оставь большой
            waitTimeout: 90000,
            sessionsPerBrowser: 1,
            testsPerSession: 1,

            browsers: {
                chrome: {
                    desiredCapabilities: {
                        browserName: 'chrome',
                        /*
                            Если хочется гонять в Яндекс.Браузере, то добавить:
                            version: 'yandex-browser'
                            acceptInsecureCerts: true в разделе desiredCapabilities, чтобы не ругался на сертик
                            и не забыть указать путь до Yandex.app в binary ↓
                        */
                        chromeOptions: {
                            binary: '/Applications/Chromium.app/Contents/MacOS/Chromium',
                            args: ['--no-sandbox', '--disable-gpu', '--allow-insecure-localhost',
                              process.env.AT_HEADLESS ? '--headless' : null,
                            ].filter(Boolean),
                        },
                    },
                },
            },
        },

        suiteManager: {
            caseFilter: {
               environment: '.+'
            }
        }
    };
    ```
    <details><summary>Если у вас Windows с WSL</summary>

      1. Положить файл .ginny.conf.js в папку с проектом

      2. В chromeOptions.binary указать <code>'C:\\\Users\\\USERNAME\\\AppData\\\Local\\\Chromium\\\Application\\\chrome.exe'</code>

      3. Скачать chrome driver версии 2.43 с https://chromedriver.chromium.org/ для Windows - один файл chromedriver.exe
      Можно отсюда - https://disk.yandex.ru/d/kuBS36yJfeg_vA

      4. Запустить один раз selenium (`make selenium`) по инструкции ниже из Ubuntu и остановить

      5. Зайти в папку <code>.../partnernode/node_modules/selenium-standalone/.selenium/chromedriver/</code> и заменить файл драйвера (например, `2.43-x64-chromedriver`) на скачанный в третьем пункте. У итогового файла не должно быть расширения .exe

      6. Теперь все тесты будут гоняться из Ubuntu, но при этом будет запускаться нативный ChromeDriver и Chromium
    </details>
4. В скрипт с настройками
    - `~/.bashrc или ~/.bash_profile` для `bash` (берём тот, который сработает)
    - `~/.zshrc` для `zsh`

    задать переменную окружения `GINNY_USER_CONFIG_PATH` с путем до файла из предыдущего шага. С помощью этой переменной Ginny находит уникальные настройки для локального прогона автотестов.
    ```sh
    export GINNY_USER_CONFIG_PATH="$HOME/.ginny.conf.js"
    ```
5. Перезапустить терминал для того, чтобы задалась переменная. Выполняем в терминале `echo $GINNY_USER_CONFIG_PATH`, если видим путь до ginny конфига – значит, предыдущие шаги были выполнены верно.

## Запуск

1. Зайти в директорию с `partnernode` репозиторием, в котором вы уже сделали `make`.
2. Запустить `make selenium`. У вас запустится локальный сервер с selenium'ом. С ним будет общаться Гермиона. Этот процесс нужно оставить рабочим, поэтому следующий шаг можно сделать в другой вкладке или окне терминала.
3. Запускаем автотесты через `npm run at` или `make autotest`

### Запускаем автотесты - npm или make?

Непосредственный запуск автотестов происходит с помощью файла `scripts/autotest.bash`, но запускать этот файла напрямую не приветствуется потому, что точками запуска задач разработчика являются `make` и `npm run`, а сами скрипты являются деталями реализации, которые могут меняться со временем.

Запустить автотесты можно как с помощью `make`, так и с помощью `npm run`, функционально эти оба способа почти равнозначны, различается только способ передачи параметров: для `make` параметры задаются через переменные среды, а для `npm run` как обычные параметры запуска скрипта - здесь каждый волен выбрать то, что ему удобнее.

### Способы фильтрации запускаемых тестов

По умолчанию запускаются **все** тесты, что долго и неудобно, поэтому при разработке и отладке нужно явно ограничить скоуп запуска. Ограничения можно задать двумя способами - через `ginny.conf.js` и через параметры скриптов. Общий подход заключается в ограничении через параметры потому, что этот вариант более прозрачен и гибок, чем файл `ginny.conf.js`. Лучше явно убедиться, что в `ginny.conf.js` фильтры отключены перед запуском своих тестов.

Если всё-таки хочется использовать фильтрацию через `ginny.conf.js`, то можно ознакомиться с [документацией](https://github.yandex-team.ru/market/hermione-suite-manager#object-casefilter).

### Настрйки фильтрации запускаемых тестов

Команды, указанные на одном уровне, являются функциольно аналогичными, если не указано другое.

Варианты фильтрации для `npm run at` и `make autotest`:
- по id теста
  - один тест
    - `npm run at -- marketmbi-1234`
    - `AT_ID="marketmbi-1234" make autotest`
  - несколько тестов
    - `npm run at -- marketmbi-1234 marketmbi-2345 marketmbi-3456`
    - `AT_ID="marketmbi-1234|marketmbi-2345|marketmbi-3456" make autotest`
- по issue id
  - одна задача
    - `npm run at -- MARKETPARTNER-12345`
    - `AT_ISSUE=MARKETPARTNER-12345 make autotest`
  - несколько задач
    - `npm run at -- MARKETPARTNER-12345 MARKETPARTNER-23456 MARKETPARTNER-19999`
    - `AT_ISSUE="MARKETPARTNER-12345|MARKETPARTNER-23456|MARKETPARTNER-19999" make autotest`
- по названию теста
  - `AT_TITLE="Синяя сводка" npm run at`
  - `AT_TITLE="Синяя сводка" make autotest`
- по feature
  - `npm run at -- -f "Агентские премии за запуски"`
  - `AT_FEATURE="Агентские премии за запуски" make autotest`
- [caseFilter](https://github.yandex-team.ru/market/hermione-suite-manager#object-casefilter)
  - `AUTOTESTS_HERMIONE_CASE_FILTER='{"id":"marketmbi-123"}' npm run at`
  - `AUTOTESTS_HERMIONE_CASE_FILTER='{"id":"marketmbi-123"}' make autotest`

Дополнительные опции:
- запустить тесты с указанием cocon commit id
  - `npm run at -- 305853080854e957cceced4e3841d944112d50cd`
  - `COCON_COMMIT_ID=305853080854e957cceced4e3841d944112d50cd make autotest`
- прогон по [скип-паку](https://github.yandex-team.ru/market/partner-hermione-tests-config)
  - игнорировать скип-пак
    - `npm run at -- -a`
    - `HERMIONE_CASES_SELECTION=all npm run at`
    - `HERMIONE_CASES_SELECTION=all make autotest`
  - только тесты из скип-пака
    - `HERMIONE_CASES_SELECTION=skipped npm run at`
    - `HERMIONE_CASES_SELECTION=skipped make autotest`
  - все тесты, кроме входящих в скип-пак (поведение по умолчанию)
    - `HERMIONE_CASES_SELECTION=default npm run at`
    - `HERMIONE_CASES_SELECTION=default make autotest`
- отключение вывода описания шагов/проверок в консоль
  - `npm run at -- -s`
  - `AT_SILENT=1 make autotest`
- задание урла целевого стенда
  - **ВАЖНО**: для правильной работы нужно закомментировать поле `baseUrl` в `~/.ginny.conf.js`!!!
  - упрощенный запуск на логрусе
    - `npm run at -- logrus01ed` - для построения урла будет взято имя текущего пользователя `whoami`, например, если `whoami` вернёт `feoktistov`, то будет построен урл `https://feoktistov.partner.market.comp.logrus01ed.yandex.ru/`
    - `AT_BASE_URL=logrus01ed make autotest` - аналогично
  - на произвольном стенде
    - `npm run at -- https://feoktistov.partner.market.comp.logrus01ed.yandex.ru/`
    - `AT_BASE_URL=https://feoktistov.partner.market.comp.logrus01ed.yandex.ru/ make autotest`
  - на престейбле
    - `npm run at -- prestable`
    - `AT_BASE_URL=prestable make autotest`
  - на БТ/fslb (поведение по умолчанию)
    - `npm run at -- fslb`
    - `AT_BASE_URL=fslb make autotest`
- включение headless-режима для браузера при прогоне АТ
  - `npm run at -- -i`
  - `AT_HEADLESS=1 make autotest`
  - эта функциональность будет работать только, если добавлен блок `args` в `~/.ginny.config.s` - см. ниже
- запуск с кадавром
  - с общим кадавром
    - `npm run at -- -k 1`
    - `KADAVR=1 make autotest`
  - со своим кадавром
    - `npm run at -- -k logrus01ed.market.yandex.net:23456`
    - `export KADAVR=1; export kadavr_host=logrus01ed.market.yandex.net; export kadavr_port=12345; make autotest`
- запуск тестов из файлов
  - `npm run at -- -e client.next/pages/Banners/spec/e2e/index.js`
  - `AT_ENTRY=client.next/pages/Banners/spec/e2e/index.js make autotest`
  - в обоих случаях можно передавать и несколько файлов, разделив их запятой, например, `client.next/pages/Banners/spec/e2e/index.js,client.next/pages/BadUrls/spec/e2e/index.js`

Нюансы:
- при перечислении нескольких значений в переменных среды нужно использовать `|` в качестве разделителя
- одновременное задание нескольких параметров
  - для `npm run at` параметры можно передавать в любом порядке,  например, `npm run at -- marketmbi-1234 -i marketmbi-2345 logrus01ed MARKETPARTNER-23456`
  - для `make autotest` параметры нужно объявить с помощью `exports` с разделением через `;` до вызова `make`, например, `export AT_ID="marketmbi-1234|marketmbi-2345"; export AT_ISSUE=MARKETPARTNER-23456; export AT_BASE_URL=https://feoktistov.partner.market.comp.logrus01ed.yandex.ru/; export AT_HEADLESS=1; make autotest`
- для возможности запускать при прогоне АТ браузер в headless-режиме нужно в `~/.ginny.conf.js` в секции `hermione.browsers.chrome.desiredCapabilities.chromeOptions` добавить поле `args`:
  ```javascript
  module.exports = { hermione: { browsers: { chrome: { desiredCapabilities: { chromeOptions: {
    // ...
    // Вот эти строчки - начало!
    args: [
      process.env.AT_HEADLESS ? '--headless' : null,
    ].filter(Boolean),
    // Вот эти строчки - конец!
    // ...
  }, }, }, }, }, };
  ```
- `npm run at` помимо параметров вызова поддерживает все переменные среды, которые актуальны для `make autotest` ровно в том же объёме
- если тест открывает Яндекс.Браузер, то страница может не загрузиться и ругаться на сертификат (в консоле) `net::ERR_CERT_INVALID`, для этого нужно добавить в `.ginny.conf.js` поле `acceptInsecureCerts: true` в разделе `desiredCapabilities`.

## Kadavr

Есть два способа запустить автотесты с кадавром ~~легкий~~ на тестинге и ~~сложный~~ на логрусе(обычно включает в себя доработку самого кадавра).

### Как запустить тесты с кадавром на тестинге

Это делается в 3 шага.

#### Шаг первый

Для этого нужно добавить `environment` для того чтобы сьюты с кадавровыми тестами не отфильтровывались.

```js
module.exports = {
    baseUrl: 'https://partner.market.fslb.yandex.ru/',
    suiteManager: {
        caseFilter: {
            environment: ‘.+’, // важно
        }
    },
    /* остальное */
}
```

#### Шаг второй

Запускаем локально selenium

```sh
cd path/to/partnernode
make selenium
```

#### Шаг третий

Запускаем автотесты

```sh
cd path/to/partnernode
KADAVR=1 make autotest
```

### Как запустить тесты с кадавром на логрусе

Важно: при разработке могут возникать сложности с тем, что изменения в коде кадавра не подхватываются, перезапускайте его, если кажется, что все должно работать, но не работает.

Добавляем/перезаписываем следующие поля в локальном конфиге `~/.ginny.conf.js`:

```js
module.exports = {
    // Тесты должны проходить на вашем логрусе
    baseUrl: 'https://<USERNAME>.partner.market.node.logrus01ed.yandex.ru/',
    kadavr: {
        host: 'logrus01ed.market.yandex.net',
        port: 12345, // любой свободный порт на логрусе,
        noSessionLog: true, // не писать логи сессии (необязательный). Отключаются ради оптимизации ресурсов сервера кадавра
    },
    suiteManager: {
        caseFilter: {
            environment: ‘.+’, // важно
        }
    },
    /* остальное */
}
```

Далее запускается все параллельно в нескольких терминалах или вкладках терминала.

#### Терминал #1

##### Установка

Разворачиваем кадаврик на логрусе (делается один раз)

```sh
ssh logrus
git clone git@github.yandex-team.ru:market/kadavrique.git # если ранее не клонировали
cd kadavrique
npm install
```

##### Запуск

Запускаем кадаврик на логрусе

```sh
ssh logrus
cd kadavrique
npm start -- --port 12345 --proxy-port 12346 --ui-port 12347
```
После чего увидим как запустилось приложение кадаврика.

Отметим что порты из примера случайные и могут быть заняты, их можно подбирать [методом тыка](https://media.github.yandex-team.ru/user/5825/files/20470b80-9f6d-11ea-958d-25e7dea828aa). Порт `--port` стоит указывать такой же как в ginny конфиге.

По умолчанию уровень логирования кадавра на логрусе имеет значение `error`, то есть в консоль будут выводится только ошибки. Чтобы сделать кадавр более информативным, нужно либо установить переменную среды `NODE_ENV` со значением `development`, тогда будет использоваться уровень `trace`, либо вручную задать нужный уровень логирования с помощью параметра `--log-level`:
```
npm start -- --port 12345 --proxy-port 12346 --ui-port 12347 --log-level info
```

#### Терминал #2

Запускаем нодное приложение

```sh
ssh logrus
cd node.partner.market_USERNAME # подставить ваш ник
export KADAVR_HOSTS="logrus01ed.market.yandex.net:12345" # тот же порт, что и в ginny конфиге
make dev-server
```

#### Терминал #3

Запускаем локально selenium

```sh
cd path/to/partnernode
make selenium
```

#### Терминал #4

Запускаем локальную сборку

```sh
cd path/to/partnernode
npm run dev --pages=page,another-page,yet-another-page
```

#### Терминал #5

Запускаем сами автотесты.

```sh
export KADAVR_HOSTS="logrus01ed.market.yandex.net:12345";
KADAVR=1 make autotest
# или если нужно запустить конкретный тест
KADAVR=1 AT_ID="marketmbi-123" make autotest
```

Подробнее как запускать конкретные тесты можно прочитать [тут](#как-фильтровать-запуск-автотестов-с-помощью-переменных-окружения).

### Вносим правки в моки кадавра

Это нужно для того что сделать ручку и бекенд "мокаемый".

1. Опционально знакомимся/вспоминаем [официальный кукбук кадавра](https://wiki.yandex-team.ru/Market/Verstka/KadavrCookBook/), чтобы знать, что и где нужно править.
2. Создаём новую ветку в репозитории кадавра от свежего мастера.
3. Вносим свои правки в моки кадавра.
4. Запускаем кадавр на логрусе на базе нашей новой ветки, отлаживаем тесты.
5. Создаём ПР в мастер кадавра, проходим ревью.
6. Мерджим ПР в мастер после получения оков.
7. Следим за автоматическим [релизным пайплайном кадавра](https://tsum.yandex-team.ru/pipe/projects/market-frontech/delivery-dashboard/market-kadavr-stages) и ждём релиза наших правок - после этого они будут доступны при прогонах АТ на стендах.

Правки в код кадавра и новую ветку можно вносить разными способами:
- Локально: настроить синк в вашем любимом редакторе с развернутым репозиторием кадавра на логрусе(аналогично процессу разработки серверной части в partnernode);
- Удаленно: создаём ветку на логрусе, делаем правки с любым консольным редактором, коммитим, пушим;
- На любителя: создаём ветку локально на ноуте, делаем правки удобным способом, пушим, на логрусе подтягиваем и перезапускаем кадавр.
