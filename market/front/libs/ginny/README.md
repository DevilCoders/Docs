Ginny
=======

Фреймворк для автоматического тестирования.

## Index

- [Description](https://github.yandex-team.ru/market/ginny#description)
- [Quick start](https://github.yandex-team.ru/market/ginny#quick-start)
- [Installing](https://github.yandex-team.ru/market/ginny#installing)
- [Uninstalling](https://github.yandex-team.ru/market/ginny#uninstalling)
- [Configuring](https://github.yandex-team.ru/market/ginny#configuring)
  - [General settings for Ginny and Hermione](https://github.yandex-team.ru/market/ginny#general-settings-for-ginny-and-hermione)
  - [Selenium Standalone Server](https://github.yandex-team.ru/market/ginny#selenium-standalone-server)
  - [Hermione](https://github.yandex-team.ru/market/ginny#hermione)
    - [Suite Manager](https://github.yandex-team.ru/market/ginny#hermione-suite-manager)
    - [Allure Reporter](https://github.yandex-team.ru/market/ginny#hermione-allure-reporter)
    - [Page Object](https://github.yandex-team.ru/market/ginny#hermione-page-object)
  - [Gemini](https://github.yandex-team.ru/market/ginny#gemini)
  - [Commands](https://github.yandex-team.ru/market/ginny#commands)
  - [Chai](https://github.yandex-team.ru/market/ginny#chai)
- [Programming API](https://github.yandex-team.ru/market/ginny#programming-api)
- [Command Line Interface](https://github.yandex-team.ru/market/ginny#command-line-interface)
  - [Usage](https://github.yandex-team.ru/market/ginny#usage)
  - [Options](https://github.yandex-team.ru/market/ginny#options)
  - [Commands](https://github.yandex-team.ru/market/ginny#commands-1)
    - [allure](https://github.yandex-team.ru/market/ginny#allure-clearbuildopen)
    - [hermione](https://github.yandex-team.ru/market/ginny#hermione-options-paths)
- [Debugging](https://github.yandex-team.ru/market/ginny#debugging)
  - [NodeJS Debugger](https://github.yandex-team.ru/market/ginny#nodejs-debugger)
  - [WebdriverIO Debugger](https://github.yandex-team.ru/market/ginny#webdriverio-debugger)
- [Environment variables](https://github.yandex-team.ru/market/ginny#environment-variables)
  - [External](https://github.yandex-team.ru/market/ginny#external)
- [Useful links](https://github.yandex-team.ru/market/ginny#useful-links)

## Description:
Ginny предоставляет програмную среду для создания, выполнения и анализа [функциональных тестов](https://en.wikipedia.org/wiki/Functional_testing), а так же [тестов на пользовательский интерфейс](https://en.wikipedia.org/wiki/Graphical_user_interface_testing).
 
Тестирование сценариев поведения осуществляется утилитой [Hermione](https://github.com/gemini-testing/hermione/), которая основанна на [WebdriverIO](http://webdriver.io/) с применением фреймворка [Mocha](https://mochajs.org/).
 
Организовать структуру файлов интеграционных тестов можно с помощью API плагина [hermione-suite-manager](https://github.yandex-team.ru/market/hermione-suite-manager).
 
Для более предметного описания тест-кейсов, в Ginny включен плагин [hermione-page-object](https://github.yandex-team.ru/market/hermione-page-object), в котором предоставлен класс [PageObject](https://github.yandex-team.ru/market/hermione-page-object#exports), имплементирующий одноименный [паттерн](http://webdriver.io/guide/testrunner/pageobjects.html).
 
С помощью библиотеки [Chai](http://chaijs.com/), предоставляемой плагином [hermione-chai](https://github.yandex-team.ru/market/hermione-chai), простым и удобным способом можно совершать проверки значений в функциональных тестах, а так же расширять API Chai собственными методами.
 
Если вы предполагаете создавать и применять [пользовательские команды](http://webdriver.io/guide/usage/customcommands.html) WebdriverIO, Ginny автоматически добавит их к объекту [browser](http://webdriver.io/guide/testrunner/browserobject.html), если определен путь к ним в соответствующей секций файла конфигурации. [Общие команды](https://github.yandex-team.ru/market/webdriver-io-commands), не имеющие привязки к сервису, уже включены в Ginny по-умолчанию, и доступны для использования.

Отчет о запуске Hermione-тестов формируется плагином [hermione-allure-reporter](https://github.yandex-team.ru/market/hermione-allure-reporter) в директорию проекта, из которого запускаются тесты. Сгенерированный отчет можно собрать и посмотреть локально, используя команды CLI Ginny, или выгрузить на один из удаленных сервисов [Allure](http://allure.qatools.ru/).

Тестирование пользовательского интерфейса так же осуществляется с помощью hermione, с использованием метода [assertView](https://github.com/gemini-testing/hermione#assertview) путем сравнения элементов web-страниц с их эталонными снимками.

Все перечисленные возможности становятся доступны после их конфигурирования в едином [файле конфигураций](https://github.yandex-team.ru/market/ginny#configuring).

Запуск [selenium-сервера](https://github.com/vvo/selenium-standalone/), тестов и других утилит, предоставляемых Ginny, осуществляется через общий [интерфейс командной строки](https://github.yandex-team.ru/market/ginny#command-line-interface).

## Quick start:
Пример минимальной конфигурации для начала приемнения интеграционного тестирования в вашем проекте с использованием Ginny:

1. Установите Ginny или добавьте в зависимости к вашему проекту: `npm install git://github.yandex-team.ru/market/ginny`.
   *(см. дополнительные требования при установке на Mac'e)*
1. В корне проекта создайте конфигурационный файл `.ginny.conf.js` со следующим содержимым:
    
    ```js
    module.exports = {
        baseUrl: 'https://market.yandex.ru/',
        hermione: {
            sets: {
                common: {
                    files: 'spec/*.hermione.js'
                }
            },
            browsers: {
                chrome: {
                    desiredCapabilities: {
                        browserName: 'chrome'
                    }
                }
            }
        }
    }
    ```
1. Создайте файл `spec/test.hermione.js` с содержимым интеграционного теста, например:
    
    ```js
    describe('feature', function () {
        it('market.yandex.ru must be available', () => {
            return this.browser.url(this.browser.options.baseUrl);
        });
    });
    ```

    Если предполагается использование плагина [hermione-suite-manager](https://github.yandex-team.ru/market/hermione-suite-manager), код теста должен быть написан с использованием интерфейса [exports](http://mochajs.org/#exports).

1. Установите и запустите selenium-сервер: `./node_modules/.bin/ginny selenium install; ./node_modules/.bin/ginny selenium start`.
1. В новой сессии терминала запустите тесты: `./node_modules/.bin/ginny hermione`. Там же будет показан некрасивый отчет о результатах прогона.
1. После завершения можно собрать и посмотреть красивый отчет: `./node_modules/.bin/ginny allure build; ./node_modules/.bin/ginny allure open`.
1. PROFIT!!!

## Installing
Для установки на Mac требуется присутствие [XCode](https://itunes.apple.com/ru/app/xcode/id497799835?mt=12) в системе. Если XCode устанавливается впервые, не забудте запустить его для подтверждения лицензии. После этого в систему будут добавлены консольные утилиты, необходимые для работы `node gyp`, используемой при установке зависимостей Ginny. В дальнейшем запуски XCode не потребуются.

Вам также потребуется установить [JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) (зависимость для Allure).

Рекомендуется использовать локальную установку: `npm install git://github.yandex-team.ru/market/ginny`.

Если возникнет необходимость, Ginny так же может быть установлена глобально.

В случае, когда Ginny запускается из под [NVM](https://github.com/creationix/nvm), необходимо добавить симлинк Ginny в локальный проект: `cd node_modules && npm link ginny`.

## Uninstalling
Для удаление Ginny и всех его зависимостей используйте команду: `npm uninstall ginny` или `npm uninstall --global ginny`, если использовалась глобальная установка.

## Configuring
Конфигурация Ginny - это конфигурация утилит и плагинов, которые в него включены.

Настройки Ginny должны находиться в файле, являющимся [NodeJS-модулем](https://nodejs.org/api/modules.html#modules_file_modules). Обычно это JSON файл или модуль, экспортирующий JavaScript-объект.

Путь к файлу настроек определяется по следующему приоритету (в порядке убывания):

1. Значение опции командной строки `-c|--config`.
1. Значение переменной окружения `GINNY_CONFIG_PATH`.
1. Файл `.ginny.conf.json` в текущей рабочей директории.

В случае, если вы захотите переопределить значения параметров из основного файла настроек, вы можете создать отдельный пользовательский конфигурационный файл, который будет иметь наивысший приоритет. Применение пользовательского конфига позволяет избежать внесения изменений в файл основных настроек проекта, а так же случайного попадания нежелательных изменений в систему контроля версий. При этом, пользовательский конфигурационный файл не заменяет, а дополняет основной, поэтому вы можете указывать там только те параметры, которые требуют изменения. Для указания пути к пользовательскому конфигурационному файлу используйте [переменную окружения](https://github.yandex-team.ru/market/ginny#environment-variables) `GINNY_USER_CONFIG_PATH`.

### General settings for Ginny and Hermione

___

NB: основная часть настроек переехала в отдельный файл-конфиг для `hermione`.

#### `{string} hermione`
**Default:** `.hermione.conf.js`
Абсолютный путь до [файла конфигурации hermione](https://github.com/gemini-testing/hermione#hermioneconfjs).

#### `{string} screenshotsDir`
Путь до папки, в которую будут складываться скриншоты, сделанные с помощью `assertView`.

#### `{Object} system`
Общие опции.

##### `{boolean} debug`
Флаг для выводы дополнительного логирования: информации о переменных окружения, cli-опциях и финализированном конфиге.

### Hermione Allure Reporter
___

#### `{Object} allure`
Настройки плагина [hermione-allure-reporter](https://github.yandex-team.ru/market/hermione-allure-reporter). Необязательная секция.

[Описание значений](https://github.yandex-team.ru/market/hermione-allure-reporter#configuration).

В этой секции доступна дополнительная опция:

##### `{string} allure.reportDir`
**Default:** `allure-report`

Путь к директории, куда будет генерироваться конечный отчет относительно рабочей директории.

##### `{string} allure.targetDir`
Путь к директории c результатами работы плагина относительно рабочей директории.

### Commands

___

#### `{Object} commands`
Настройки автоматической загрузки [пользовательских команд](http://webdriver.io/guide/usage/customcommands.html) Webdriver-а. Необязательная секция.

По-умолчанию в Ginny уже включены [общие кроссервисные команды](https://github.yandex-team.ru/market/webdriver-io-commands), даже если секция `commands` не определена.

##### `{string|string[]} commands.targetDir`
Путь или массив путей к папкам, содержащим файлы реализаций пользовательских команд относительно рабочей директории. Рекурсивная загрузка не поддерживается.

## Programming API
### Importing:
`const ginny = require('ginny');`

### Classes:
#### `{Function} ginny.PageObject`
Класс [PageObject](https://github.yandex-team.ru/market/hermione-page-object#exports).

#### `{Function} ginny.ErrorHandler`
Класс [ErrorHandler](https://github.com/webdriverio/webdriverio/blob/master/lib/utils/ErrorHandler.js).

### Methods:
#### `{Function} ginny.importSuite`
Метод [suiteManager.import](https://github.yandex-team.ru/market/hermione-suite-manager#importrelativepath--decl).

#### `{Function} ginny.mergeSuites`
Метод [suiteManager.merge](https://github.yandex-team.ru/market/hermione-suite-manager#mergesuites).

#### `{Function} ginny.makeCase`
Метод [suiteManager.makeCase](https://github.yandex-team.ru/market/hermione-suite-manager#makecasetestcase).

#### `{Function} ginny.makeSuite`
Метод [suiteManager.makeSuite](https://github.yandex-team.ru/market/hermione-suite-manager#makesuitesuite).

## Command Line Interface
### Usage:
`ginny [options] <command> [subcommand]`

Необходимо придерживаться следующей последовательности запуска команд:

    ginny selenium install
    ginny selenium start
    ginny <hermione> <...>
    ginny <allure|testpalm> <...>

### Options:
`-h, --help` - Выводит справку по использованию CLI. Подробную информацию по каждой команде можно получить, вызвав `ginny <command> -h|--help`.

`-V, --version` - Выводит текущую версию Ginny.

`-c, --config [path]` - Устанавливает путь до файла конфигурации Ginny.

### Commands:
#### `allure <clear|build|open>`
Управление отчетом [Allure](http://allure.qatools.ru/).

##### Подкоманды:

- `clear` - Рекурсивно очищает директории `allure.targetDir` и `allure.reportDir`.
- `build` - Генерирует отчет Allure из `allure.targetDir` в `allure.reportDir`.
- `open` - Открывает в браузере сгенерированный отчет Allure из директории `allure.reportDir`.

___

#### `hermione [options] [paths...]`
Запускает Hermione-тесты. Для этой команды доступна дополнительная опция:

`-H, --hermione-options "<options>"` - Устанавливает опции запуска для Hermione (имеют приоритет выше, чем у параметров из конфигурационного файла). Список поддерживаемых опций можно посмотреть [здесь](https://github.com/gemini-testing/hermione/#cli).

Так же поддерживаются опции переопределения значений, установленных в конфигурационном файле Ginny, например: `ginny hermione --base-url "https://example.com/"`. Подробнее о переопределении настроек Hermione [здесь](https://github.com/gemini-testing/hermione/#overriding-settings).

После опций можно указать пути к файлам тестовых сценариев, которые должны быть выполнены. Переданные пути должны соответствовать маске файлов тестовых сценариев, указанные в опции `hermione.sets.<platform>.files`.

___

#### `selenium <install|start>`
Управление selenium-сервером.

##### Подкоманды:

 - `install` - Устанавливает драйверы к браузерам для Selenium Standalone Server с применением параметров из конфигурационного файла.
 - `start` - Запускает Selenium Standalone Server с применением параметров из конфигурационного файла.

___

#### `testpalm <import_run>`
Интеграция с сервисом [TestPalm](http://testpalm.yandex-team.ru/). Для работы команда требует указания двух обязательных опций:

`-P, --project <project>` - Имя проекта в TestPalm.

`-T, --token <token>` - API токен TestPalm.

##### Подкоманды:

 - `import_run` - Импортирует ран из файла в TestPalm. Для импорта необходимо указать опцию:
   - `-R, --run <run_file>` - Путь к файлу с раном.
 Перед импортом имеется возможность наложить пач на данные рана, находящиеся в исходном файле. Для этого необходимо сохранить пач в формате JSON в переменную окружения `GINNY_TESTPALM_RUN_PATCH`.

___

#### `kadavr <start>`
Управление [Кадавриком](https://github.yandex-team.ru/market/kadavrique).

##### Подкоманды:

 - `start` - Запускает HTTP-сервер Кадаврика. При запуске можно указать дополнительные опции Кадаврика.

## Debugging
### NodeJS Debugger
#### Пример настройки отладчика интеграционных тестов для редакторов IDEA/WebStorm:

1. Открыть настройки отладчика: **Run → Edit Configurations...**
1. Создать новый профиль: **Add New Configuraion (+) → Node.js**
1. Заполнить следующие поля:

    - **Name**: `Ginny Debugger` (или выбрать по вкусу)
    - **Node interpreter**: Убедиться, что выбрана версия интерпретатора `v.6.9.5`, например: `~/.nvm/versions/node/v6.9.5/bin/node`
    - **Node parameters**: Пустое значение.
    - **Working directory**: Абсолютный путь к корню вашего проекта, из которого запускаются тесты.
    - **JavaScript file**: Абсолютный путь к исполняемому файлу Ginny, например: `/home/<username>/.nvm/versions/node/v6.9.5/bin/ginny`
    - **Application parameters**: `hermione`. Здесь так же могут быть указаны другие параметры [CLI Ginny](https://github.yandex-team.ru/market/ginny#command-line-interface).
    - **Environment variables**: Переменные окружения:
      - **GINNY_CONFIG_PATH**: Путь к конфигурационному файлу Ginny относительно значения *Working directory*.
      - *(при необходимости)* **GINNY_USER_CONFIG_PATH**: Путь к пользовательскому конфигурационному файлу Ginny относительно значения *Working directory*.
      - *(при необходимости)* **NODE_PATH**: Абсолютный путь к директории глобальных npm-модулей, например: `/home/<username>/.nvm/versions/node/v6.9.5/lib/node_modules`.

1. Сохранить настройки: **OK**
1. Увеличить [таймаут](https://mochajs.org/#t---timeout-ms) ожидания теста для Mocha в секции конфигурации Hermione:

  ```
  hermione: {
      system: {
          mochaOpts: {
              timeout: 9999999
          }
      }
  }
  ```

#### Пример настройки отладчика для Visual Studio Code:

Добавить в конфигурацию отладчика `launch.js` соответствующие настройки, например:
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Ginny Debugger",
            "program": "${workspaceFolder}/node_modules/.bin/ginny",
            "args": [
                "hermione"
            ],
            "showAsyncStacks": true,
            "env": {
                "GINNY_CONFIG_PATH": "./configs/current/ginny.conf.js",
                "GINNY_USER_CONFIG_PATH": "/Users/your_user_name/.ginny.conf.js"
            }
        }
    ]
}
```

Переменная `GINNY_USER_CONFIG_PATH` должна ссылаться на ваш личный конфиг.

Опция `program` в примере подразумевает, то что `ginny` слинкован в `node_modules` тестируемого проекта или установлен локально.

Настройка отладчика для других IDE и редакторов осуществляется аналогичным образом.

### WebdriverIO Debugger

В случаях, если необходимо залезть "в кишки", посмотреть на запросы, отправляющиеся в selenium-грид и т.д., тогда надо воспользоваться WebdriverIO Debugger, но как правило это не нужно.

Для получения информации об отладке средствами WebdriverIO обратитесь к [этому документу](http://webdriver.io/guide/testrunner/debugging.html).

Для включения режима отладки WebdriverIO установите значение `true` для опции [hermione.system.debug](https://github.com/gemini-testing/hermione/#debug) в конфигурационном файле Ginny.

## Environment variables

### `GINNY_CONFIG_PATH`
Путь к конфигурационному файлу Ginny.

### `GINNY_USER_CONFIG_PATH`
Путь к пользовательскому конфигурационному файлу Ginny. Значения, указанные в этом файле, имеют наивысший приоритет.

### External:

 - [HERMIONE_SKIP_BROWSERS](https://github.com/gemini-testing/hermione/#hermione_skip_browsers)
 - [Переопределение настроек Hermione](https://github.com/gemini-testing/hermione/#overriding-settings)
 - [Переопределение настроек Gemini](https://github.com/gemini-testing/gemini/blob/master/doc/config.md#overriding-settings)

## Useful links:

- [WebriverIO](http://webdriver.io/)
- [Selenium Standalone](https://github.com/vvo/selenium-standalone/)
- [Mocha](https://mochajs.org/)
- [Chai](http://chaijs.com/)
- [Chai Assertions for Promises](https://github.com/domenic/chai-as-promised/)
