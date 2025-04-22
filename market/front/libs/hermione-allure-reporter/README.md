Hermione Allure Reporter
=======

## Index

- [Description](https://github.yandex-team.ru/market/hermione-allure-reporter#description)
  - [Features](https://github.yandex-team.ru/market/hermione-allure-reporter#features)
- [Configuration](https://github.yandex-team.ru/market/hermione-allure-reporter#configuration)
- [Overriding Settings](https://github.yandex-team.ru/market/hermione-allure-reporter#overriding-settings)
- [Using](https://github.yandex-team.ru/market/hermione-allure-reporter#using)
- [API](https://github.yandex-team.ru/market/hermione-allure-reporter#api)
  - [Programming](https://github.yandex-team.ru/market/hermione-allure-reporter#programming)
    - [allure](https://github.yandex-team.ru/market/hermione-allure-reporter#allure)
      - [Properties](https://github.yandex-team.ru/market/hermione-allure-reporter#properties)
      - [Methods](https://github.yandex-team.ru/market/hermione-allure-reporter#methods)

## Description
Плагин для [Гермионы](https://github.com/gemini-testing/hermione/), генерирующий отчет [Allure](https://docs.qameta.io/allure/latest/).
 
### Features:

- Использует последнюю версию [Allure 2.0](https://docs.qameta.io/allure/latest/).
- Поддерживает параллельный прогон тестов.
- Предоставляет [API](https://github.yandex-team.ru/market/hermione-allure-reporter#api) для управления данными теста в отчете.
- Поддерживается [интеграция](https://github.yandex-team.ru/market/hermione-allure-reporter#boolean-patchchai) с интерфейсом [chai.assert](http://chaijs.com/api/assert/) для автоматического создания [шагов](https://github.com/allure-framework/allure1/wiki/Glossary#test-step) при обращении к его методам.
- Разделяет кейсы по сессиям, формируя график выполнения тестов на вкладке `Timeline`.
- Добавляет информацию об [окружении](https://github.yandex-team.ru/market/hermione-allure-reporter#programming-api):
    - `Browser` - Имена и версии используемых браузеров.
    - `Base URL` - Базовый URL тестов.
    - `Grid URL` - URL Selenium-грида.
    - `Environment` - Окружение, в котором выполнялись тесты: `development`, `testing` или `production`.
- Позволяет передавать мета-информацию из тестов в отчет, привязанную с помощью [методов Hermione](https://github.com/gemini-testing/hermione/#sharable-meta-info) или плагина [hermione-suite-manager](https://github.yandex-team.ru/market/hermione-suite-manager#makecasetestcase):
    - `{string} suitePath` - Путь к файлу, в котором находится тест. Используется при группировке по файлам во вкладке `Packages`.
    - `{string} [feature]` - Имя фичи. Используется при группировке по фичам во вкладке `Behaviors`.
    - `{string} [id]` - Номер кейса в менеджере тестов. Для того, что бы в отчете тестов сформировалась ссылка на менеджер тестов, должна быть установлена опция `testsManagementPattern` в настройках плагина.
    - `{string} [issue]` - Номер тикета в менеджере тикетов. Для того, что бы в отчете тестов сформировалась ссылка на менеджер тикетов, должна быть установлена опция `issuesTrackerPattern` в настройках плагина.
    - `{string} [severity]` - Приоритет теста в соответствии с [`allure.SEVERITY`](https://github.yandex-team.ru/market/hermione-allure-reporter#object-const-severity).
    - `{string} [description]` - Описание кейса в формате Markdown.
    - `{Object} [params]` - Аргументы теста: список параметров, которые тест использует из `this.params`. Ключи соответствуют ключам из `this.params`, а значениям соответствуют человекопонятные описания параметров. В отчете будут сформированы параметры, состоящие из их описаний и значений, содержащихся в `this.params` по соответствующему ключу.
- Позволяет добавить информацию о внешнем сервисе, запустившим прогон тестов: имя сервиса, заголовок и ссылку на запуск.
- Умеет экспортировать результаты прогона в сервис [TestPalm](https://testpalm.yandex-team.ru/) или в файл `.json` в виде [рана](https://wiki.yandex-team.ru/testpalm/testpalmdoc/run/). В ран экспортируются только те кейсы, у которых указан `id` в мета-информации. Кейсы в ране группируются по родительским фичам (мета `feature`), в которых содержится тест. Ран содержит в себе информацию об окружении, а так же информацию о сервисе, в котором создавался отчет, если это было указано в параметрах плагина.
- Прикрепляет дополнительную отладочную информацию к упавшему тесту:
    - `Screenshot` - снимок экрана в момент ошибки (если не было отключено в параметрах плагина)
    - `Kadavr log` - логи запросов/ответов к кадавровым бэкендам (для поломанных тестов)
    - `Last WD Commands` - последние пять команд от WebdriverIO к селениуму
    - `Test Meta` - мета-информация теста
    - `WD Options` - опции WebdriverIO
    - `Desired Capabilities` - параметры браузера
    - `Session ID` - ID сессии в селениум-гриде
- Поддерживается [переопределение опций](https://github.yandex-team.ru/market/hermione-allure-reporter#overriding-settings) плагина с помощью параметров запуска приложения или переменных окружения.

## Configuration
Параметры:

#### `{function} resolveStatus`
**Default: `error => {
    return () => {
        return error.name === 'AssertionError' ? ALLURE_STATUS.failed : ALLURE_STATUS.broken;
    };
}`**

Функция для выбора статуса при падении теста

___

#### `{string} testsManagementPattern`
**Default: `undefined`**

Паттерн URL менеджера тестов, например `http://tms.company.com/tests/%s`, где вместо `%s` будет подставлен номер теста.

___

#### `{string} issuesTrackerPattern`
**Default: `undefined`**

Паттерн URL менеджера тикетов, например `http://github.com/allure-framework/allure-core/issues/%s`, где вместо `%s` будет подставлен номер тикета.

___

#### `{boolean} patchChai`
**Default: `true`**

Патчит интерфейс [chai.assert](http://chaijs.com/api/assert/). При любом обращении к методам интерфейса автоматически будет создаваться соответствующий [шаг](https://github.com/allure-framework/allure1/wiki/Glossary#test-step) в отчете.

**Пример:**
Проверка в тесте:

```js
this
    .expect(typeof typeof true)
    .to.be.equal('string', 'typeof должен возвращать строку');
```

Сгенерированный шаг: `typeof должен возвращать строку: expected 'string' to equal 'string'`.

При этом, проверки вида `'string'.should.to.be.string` создавать шаги Allure не будут.

___

#### `{boolean} screenshotOnReject`
**Default: `true`**

Флаг, указывающий на необходимость создания скриншотов при падении теста или сьюта.

___

#### `{string} targetDir`
**Default:** `'allure-results'`

Путь к директории, куда будут генерироваться исходники для отчета, относительно рабочей директории.

___

#### `{string} reportDir`
**Default:** `'allure-report'`

Путь к директории, куда будут генерироваться конечный отчет, относительно рабочей директории.

___

##### `{Object} customAttaches`

Функции, результат которых запишется во вложение при падении.

Ключ - название вложения.

Результат выполнения - тело вложения.

```
customAttaches: {
  customAttach1: (browser) => browser.getUrl(),
}
```

___

#### `{Object} executor`

Информация о сервисе, в котором прогонялись тесты.

___

##### `{string} executor.name`
**Default:** `'Sandbox'`

Имя сервиса, в котором прогонялись тесты.

___

##### `{string} executor.title`
**Default:** `'Default title'`

Заголовок прогона. Необязательный параметр.

___

##### `{string} executor.link`

Ссылка на прогон тестов. Необязательный параметр.

___

##### `{string} executor.reportUrl`

Ссылка текущий прогон, экспортируется в ран. Необязательный параметр.

___

#### `{Object} testpalm`

Настройки интеграции с [TestPalm](https://testpalm.yandex-team.ru/):

___

##### `{string} testpalm.project`

Имя [проекта](https://wiki.yandex-team.ru/testpalm/testpalmdoc/project). Обязательный параемтр, если включен экспорт рана параметром `testpalm.run.export`.

___

##### `{string} testpalm.token`

API-токен [доступа](https://wiki.yandex-team.ru/testpalm/testpalmdoc/dostup) к TestPalm. Токен можно узнать [здесь](https://testpalm.yandex-team.ru/internal/profile). Обязательный параемтр, если включен экспорт рана параметром `testpalm.run.export`.

___

##### `{Object} testpalm.run`

Параметры экспорта [рана](https://wiki.yandex-team.ru/testpalm/testpalmdoc/run/) в TestPalm:

___

###### `{boolean} testpalm.run.export`
**Default:** `false`

Включает или отключает экспорт рана.

___

###### `{string} testpalm.run.exportToFile`
**Default:** `''`

Если опция задана, ран будет экспортирован в указанный файл. Путь к файлу задается относительно рабочей директории.

___

###### `{string} testpalm.run.version`
**Default:** `'Trash'`

[Версия](https://wiki.yandex-team.ru/testpalm/testpalmdoc/version) запуска в TestPalm. Необязательный параметр.

___

###### `{string} testpalm.run.issue`

Корневой тикет в багтрекере. Необязательный параметр.

___

###### `{string} testpalm.run.author`
**Default:** `'robot-metatron'`

Имя автора, запустившего прогон тестов. Необязательный параметр.

### Overriding Settings
Значения из конфига плагина могут быть переопределены с помощью (в порядке убывания приоритета):

1. опций командной строки (префикс `hermione-allure-`)
2. переменных окружения (префикс `hermione-allure_`)

Подробнее о конвертации параметров читайте [здесь](https://github.com/gemini-testing/hermione#overriding-settings).

## Using
В коде тестов вы можете самостоятельно управлять [сущностями Allure](https://github.com/allure-framework/allure1/wiki#main-features), используя методы объекта `allure`.

Для генерации и просмотра отчета используйте [интерфейс командной строки Allure](http://wiki.qatools.ru/display/AL/Allure+Commandline#AllureCommandline-usageUsage). Так же вы можете использовать [командный интерфейс Ginny](http://wiki.qatools.ru/display/AL/Allure+Commandline#AllureCommandline-usageUsage), если плагин используется в его составе.

## API
### Programming
Публичное API доступно в пространствве имен `allure` в контексте тестов, а так же в пространстве имен [browser](http://webdriver.io/guide/testrunner/browserobject.html) для использования в [пользоваткельских командах](http://webdriver.io/guide/usage/customcommands.html):

Пример использования в тестах:

```js
describe('Suite', function () {
    it('Case', () => {
        // Создать и выполнить шаг:
        return this.allure.runStep('Step', () => {
            // Код теста
        });
    })
})
```

Пример использования в команде WebdriverIO:

```js
browser.addCommand('My Command', function() {
  return this.allure.runStep('Step', () => {
      // Код команды
  });
});
```

___

### `allure`
Экземпляр класса [RuntimeAdapter](lib/RuntimeAdapter.js), наследующий от класса [Runtime](https://github.com/allure-framework/allure-js-commons/blob/master/runtime.js).

#### Properties:

___

##### `{Object} const SEVERITY`
Хеш значений важности теста, применяющиеся при использовании метода `allure.severity()`.

###### `{string} const SEVERITY.BLOCKER`
**Значение:** `'blocker'`
###### `{string} const SEVERITY.CRITICAL`
**Значение:** `'critical'`
###### `{string} const SEVERITY.NORMAL`
**Значение:** `'normal'`
###### `{string} const SEVERITY.MINOR`
**Значение:** `'minor'`
###### `{string} const SEVERITY.TRIVIAL`
**Значение:** `'trivial'`

#### Methods:

___

#### `isPromise(obj)`
Проверяет, является ли переданный объект промисом.

**Аргументы:**

- `{*} obj` - Проверяемый объект.

**Возвращает:**

`{boolean}` - Результат проверки.

___

#### `createStep(name, body)`
Создает [шаг](https://github.com/allure-framework/allure1/wiki/Steps) для текущего кейса.

**Аргументы:**

- `{string} name` - Имя шага.
- `{Function} body` - Тело шага.

**Возвращает:**

`{Function}` - Созданную функцию-шаг.

___

#### `runStep(name, body [, ...args])`
Создает и выполняет [шаг](https://github.com/allure-framework/allure1/wiki/Steps) для текущего кейса.

**Аргументы:**

- `{string} name` - Имя шага.
- `{Function} body` - Тело шага.
- `{*} [...args]` - Значения, которые будут переданы в тело шага в качестве аргументов.

**Возвращает:**

`{*}` - То же, что возвращает тело шага.

___

#### `createAttachment(name, content [, type])`
Создает и добавляет [вложение](https://github.com/allure-framework/allure1/wiki/Attachments) для текущего теста или шага.

**Аргументы:**

- `{string} name` - Имя вложения.
- `{string|Buffer|Function} content` - Содержимое вложения.
- `{string} [type='text/plain']` - MIME-тип вложения. Поддерживаются: `txt`, `html`, `xml`, `png`, `jpg`, `json`, `other`.

**Возвращает:**

`{Function|undefined}`

___

#### `addLabel(name, value)`
Добавляет произвольную метку в текущий кейс.

**Аргументы:**

- `{string} name` - Имя метки.
- `{string} value` - Значение метки.

___

#### `addArgument(name, value)`
Добавляет [параметр](https://github.com/allure-framework/allure1/wiki/Parameters) в текущий кейс.

**Аргументы:**

- `{string} name` - Имя аргумента.
- `{string} value` - Значение аргумента.

___

#### `addEnvironment(name, value)`
Добавляет [параметр окружения](https://github.com/allure-framework/allure1/wiki/Environment) в текущий кейс.

**Аргументы:**

- `{string} name` - Имя параметра.
- `{string} value` - Значение параметра.

___

#### `description(description [, type])`
Добавляет описание для текущего кейса.

**Аргументы:**

- `{string} description` - Описание кейса.
- `{string} [type='text']` - Тип описания. Поддерживаемые значения: `text`, `html`, `markdown`.

___

#### `severity(severity)`
Устанавливает метку уровня важности для текущего кейса.

**Аргументы:**

- `{string} severity` - Значения уровня важности.

___

#### `feature(feature)`
Устанавливает метку [фичи](https://github.com/allure-framework/allure1/wiki/Features-and-Stories) для текущего теста.

**Аргументы:**

- `{string} feature` - Название фичи.

___

#### `story(story)`
Устанавливает метку описания [фичи](https://github.com/allure-framework/allure1/wiki/Features-and-Stories) для текущего теста.

**Аргументы:**

- `{string} story` - Описание фичи.
