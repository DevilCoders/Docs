Hermione Suite Manager
=======

## Index

- [Description](https://github.yandex-team.ru/market/hermione-suite-manager#description)
- [Configuration](https://github.yandex-team.ru/market/hermione-suite-manager#configuration)
  - [Overriding Settings](https://github.yandex-team.ru/market/hermione-suite-manager#overriding-settings)
- [Testsuite Organization Example](https://github.yandex-team.ru/market/hermione-suite-manager#testsuite-organization-example)
  - [Example of Test Location in File System](https://github.yandex-team.ru/market/hermione-suite-manager#example-of-test-location-in-file-system)
  - [Hermione Configuration](https://github.yandex-team.ru/market/hermione-suite-manager#hermione-configuration)
  - [Menu Block Tests](https://github.yandex-team.ru/market/hermione-suite-manager#menu-block-tests)
  - [Root Testsuite](https://github.yandex-team.ru/market/hermione-suite-manager#root-testsuite)
  - [Result Testsuite](https://github.yandex-team.ru/market/hermione-suite-manager#result-testsuite)
- [API](https://github.yandex-team.ru/market/hermione-suite-manager#api)
  - [Test context](https://github.yandex-team.ru/market/hermione-suite-manager#test-context)
  - [Exports](https://github.yandex-team.ru/market/hermione-suite-manager#exports)
    - [Methods](https://github.yandex-team.ru/market/hermione-suite-manager#methods)

## Description
Плагин для [Гермионы](https://github.com/gemini-testing/hermione/), позволяющий организовать разделение тестов на отдельные файлы и подключать их в других тестах при необходимости. Для корректной работы требуется написания тестов с использованием интерфейса [exports](https://mochajs.org/#exports).

Для каждого тест-кейса плагин позволяет привязать мета-теги, которые сохраняются в [мета-информации](https://github.com/gemini-testing/hermione/#sharable-meta-info) теста. С помощью тегов можно отфильтровать нужные тесты для запуска, а так же использовать их в других компонентах, например в отчетах.

Импортируемые наборы тестов должны соответствовать следующим требованиям:

- Файл набора должен экспортировать объект - экземпляр класса Object.
- Экспортируемый объект должен иметь единственное свойство - корневой сьют.
- Значением корневого сьюта должен быть объект (экземпляр класса Object).

Корневой сьют может содержать в себе тесты, хуки и другие сьюты.

## Configuration
Параметры:

#### `{string} suitesDir`
Путь к директории, где располагаются наборы тестов.

#### `{Array} [metaTags]`
Массив разрешенных мета-тегов. По-умолчанию разрешены:
  - `id`: ID Кейса в менеджере тест-кейсов
  - `feature`: Имя фичи
  - `issue`: Номер тикета в менеджере тикетов
  - `environment`: Окружение, в котором выполняется тест
  - `severity`: Уровень важности в соответствии с [`allure.SEVERITY`](https://github.yandex-team.ru/market/hermione-allure-reporter#object-const-severity)
  - `description`: Описание кейса
  - `defaultParams`: Значения параметров кейсов по умолчанию
  - `params`: Значения параметров кейсов

#### `{Array} [skips]`

Массив объектов, описывающих кейсы, которые должны быть пропущены. Каждый объект должен содержать:
  - `case`: полное имя кейса
  - `reason`: причина наличия скипа
  - `issue`: тикет, в рамках которого скип должен быть убран а тест починен

#### `{Function} handleTestsTitles`

Колбэк, принимающий до начала прогона тестов массив имен всех кейсов.

#### `{Object} [caseFilter]`
Правила фильтрации тест-кейсов по мета-тегам, заданным функциями [`makeCase`](https://github.yandex-team.ru/market/hermione-suite-manager#makecasetestcase) и [`makeSuite`](https://github.yandex-team.ru/market/hermione-suite-manager#makesuitesuite). Значением параметра должен быть объект, в котором ключи соответствуют именам мета-тегов, по которым следует производить фильтрацию. Значения ключей представляют собой регулярные выражения в виде строки. В декларации могут быть указаны только те мета-теги, для которых тип значения в тесте соответствует строке. Остальные ключи будут проигнорированы.

Тесты фильтруются по следующим правилам:

- Если фильтр тестов не задекларирован, будут запущены все тесты.
- Если в фильтре тестов указан один мета-тег, будут выполнены только те тесты, в которых значение соответствующего мета-тега соответствует значению из декларации фильтра.
- Если в фильтре тестов указано несколько мета-тегов, будут выполнены только те тесты, в которых все значения соответствующих мета-тегов соответствуют их значениям из декларации фильтра.
- Мета-теги, привязанные к тесту и не указанные в фильтре тестов, будут проигнорированы.

**Примеры:**

Будут выполнены только те тесты, для которых значение мета-тега `id` равно `100` или `101`:

```js
caseFilter: {
    id: '100|101'
}
```

Будут выполнены только тесты для тикета `MARKETFRONTEND-999`, имеющие приоритет `blocker` или `critical`:

```js
caseFilter: {
    issue: 'MARKETFRONTEND-999',
    severity: 'blocker|critical'
}
```

Будут выполнены только те тесты, для которых определено окружение:

```js
caseFilter: {
    environment: '.+'
}
```

#### `{Array} [only]`

Массив строк. 
Полные тайтлы кейсов, которые необходимо выполнить.

Фильтрация совмещается с фильтрацией из `caseFilter` по логике И.

#### `{String} [metaInfoFilename]`

Путь до файла, в который будет записана мета-информация о тестах.

### Overriding Settings
Значения из конфига плагина могут быть переопределены с помощью (в порядке убывания приоритета):

1. опций командной строки:
    - `--hermione-suite-manager-suites-dir`: Параметр [`suitesDir`](https://github.yandex-team.ru/market/hermione-suite-manager#string-suitesdir).
    - `--hermione-suite-manager-meta-tags`: Параметр [`metaTags`](https://github.yandex-team.ru/market/hermione-suite-manager#array-metatags). Имена мета-тегов могут разделяться запятой или пробелом.
    - `--hermione-suite-manager-case-filter`: Параметр [`caseFilter`](https://github.yandex-team.ru/market/hermione-suite-manager#object-casefilter). Значение должно быть в формате JSON.

2. переменных окружения:
    - `hermione-suite-manager_suites_dir`: Параметр [`suitesDir`](https://github.yandex-team.ru/market/hermione-suite-manager#string-suitesdir).
    - `hermione-suite-manager_meta_tags`: Параметр [`metaTags`](https://github.yandex-team.ru/market/hermione-suite-manager#array-metatags). Имена мета-тегов могут разделяться запятой или пробелом.
    - `hermione-suite-manager_case_filter`: Параметр [`caseFilter`](https://github.yandex-team.ru/market/hermione-suite-manager#object-casefilter). Значение должно быть в формате JSON.

## Testsuite Organization Example

#### Example of Test Location in File System:

    |- spec
    |  |- suites
    |  |  |- menu.js (Набор тест-кейсов на блок menu)
    |  |
    |  |- tests
    |  |  |- test.hermione.js (Корневой файл тест-кесов)
    |
    |- .hermione.conf.js (Файл конфигурации Hermione)
    
#### Hermione Configuration:

Минимально необходимая конфигурация `.hermione.conf.js`:

```js
module.exports = {
    sets: {
        desktop: {
            // Путь к файлам тестов должен указывать на директорию корневых тест-кейсов.
            files: 'spec/tests'
        }
    },
    
    system: {
        mochaOpts: {
            // При указании параметров Mocha, значения по-умолчанию,
            // заданные в Hermione, сбрасываются.
            // Если не установить значение таймаута,
            // тетсы будут падать с ошибкой:
            // https://github.com/mochajs/mocha/blob/master/lib/runnable.js#L233
            timeout: 60000,
            
            // Поддерживается только интерфейс exports.
            ui: 'exports'
        }
    },
    
    plugins: {
        // Регистрация плагина.
        '@yandex-market/hermione-suite-manager': {
            // Путь к наборам тест-кейсов.
            suitesDir: 'spec/suites'
        }
    }
};
```

Дополнительную информацию о параметрах конфигурации Hermione можно получить [здесь](https://github.com/gemini-testing/hermione/#hermioneconfjs).

Если плагин используется в составе [Ginny](https://github.yandex-team.ru/market/ginny), параметры плагина указываются в [соответствующей секции](https://github.yandex-team.ru/market/ginny#hermione-suite-manager) его файла конфигураций.

#### Menu Block Tests:

Содержимое файла `spec/suites/menu.js`:

```js
const assert = require('assert');

module.exports = {
    'Блок "menu"': {
        before() {
            // beforeAll hook for menu
        },
        'должен присутствовать'() {
            return this.browser
                .isExisting('.menu')
                .then((result) => assert(result, 'Блок отсутствует'));
        }
    }
};
```

#### Root Testsuite:

Содержимое файла `spec/tests/test.hermione.js`:

```js
const assert = require('assert');
const suiteManager = require('@yandex-market/hermione-suite-manager');

module.exports = 
    // Объединение корневого набора с импортируемыми.
    {
        'Яндекс.Маркет': suiteManager.merge(
            {
                before() {
                    return this.browser.url('https://market.yandex.ru/');
                },
                'должен быть доступен'() {
                    return this.browser
                        .getUrl()
                        .then((url) => assert(url, 'Некорректный URL'));
                }
            },

             // Импорт внешнего набора тест-кейсов относительно пути из suitesDir.
             suiteManager.import('menu', {
                 hooks: {
                     beforeEach() {
                         // beforeEach hook for menu
                     }
                 }
             }),
             
             // Альтернативный способ импорта наборов предполагает использование
             // функции require(), если не требуется установки дополнительных хуков и
             // импортируемый набор передается в метод suiteManager.merge().
             require('../suites/menu')
         )
    };
```

#### Result Testsuite:

Результат работы API плагина будет идентичен следующему файлу тестов в представлении интерфейса [BDD](http://mochajs.org/#bdd):

```js

describe('Яндекс.Маркет', function () {
    before(function () {
        return this.browser.url('https://market.yandex.ru/');
    });
    
    it('должен быть доступен', () => {
        return this.browser
            .getUrl()
            .then((url) => assert(url, 'Некорректный URL'));
    });

    describe('Блок "menu"', function () {
        before(function () {
            // beforeAll hook for menu
        });
        
        beforeEach(function () {
            // beforeEach hook for menu
        });
        
        it('должен присутствовать', () => {
            return this.browser
                .isExisting('.menu')
                .then((result) => assert(result, 'Блок отсутствует'));
        });
    });
});
```

## API
### Test context
Плагин расширяет контекст выполнения тестов, предоставляемый [Mocha](https://mochajs.org/):

___

#### `skip([description])`
Пропускает выполнение теста или набора тестов.

**Аргументы:**
- `{string} [description]` - Текстовое описание причины отмены выполнения теста или набора тестов.

**Пример:**
```js
const suiteManager = require('@yandex-market/hermione-suite-manager');

module.exports = {
    'Яндекс.Маркет': {
        before() {
            // Отмена выполнения всех тестов в текущем наборе.
            return this.skip();
        },
        'должен быть доступен'() {
            // Отмена выполнения конкретного теста.
            return this.skip('Reason');
            
            // Test
        }
    }
};
```

### Exports

```js
const suiteManager = require('@yandex-market/hermione-suite-manager');
```

#### Methods:

___

#### `prepare(suite [, options])`
Добавление [мета-информации](https://github.com/gemini-testing/hermione/#sharable-meta-info) для сьюта.

**Аргументы:**

- `{Object} suite` - Набор тест-кейсов (сьют).
- `{SuiteOptions} [options]` - Дополнительные параметры объединения. Поддерживаются следующие ключи:
  - `{HooksDeclaration} hooks` - Объект-декларация хуков, которые будут добавлены в импортируемый набор. Поддерживаемые хуки (имена ключей): `before`, `beforeEach`, `afterEach`, `after`. Значениями ключей должны быть функции.
  - `{Object} meta` - Объект, содержащий [мета-теги](https://github.yandex-team.ru/market/hermione-suite-manager#array-metatags), которыми будут переопределена мета-теги тестов, определенных внутри импортируемого сьюта.
  - `{Object} params` - Объект параметров, который будет доступен из свойста `params` контекста тестов импортируемого набора.
  - `{Object} pageObjects` - Объект-декларация экземпляров PageObject-ов. Если декларация была указана, в импортируемом наборе будет создан хук `before`, содержищий вызов метода [PageObject.setPageObjects](https://github.yandex-team.ru/market/hermione-page-object#setpageobjectsdecl) с передачей ему переданного объекта.
  - `{Object} extend` - Расширяющий набор дополнительных проверок для импортируемого сьюта.
  - `{string|string[]}` only - строковый ключ или массив строковых ключей для фильтрации сьютов в импортируемом сьюте. При использовании будут импортированы только те сьюты, имя которых _полностью_ соответствует одному из переданных ключей.
  - `{string} suiteName` - Кастомное название. Будет использовано вместо указанного в сьюте.

**Возвращает:**

`{Object}` - Копия объекта.

___

#### `import(relativePath [, options])`
Импорт набора тест-кейсов. К каждому тесту в импортируемом наборе добавляется [мета-информация](https://github.com/gemini-testing/hermione/#sharable-meta-info) `suitePath`, содержащая путь к файлу набора.

**Аргументы:**

- `{string} relativePath` - Путь к файлу набора относительно опции [`suitesDir`](https://github.yandex-team.ru/market/hermione-suite-manager#string-suitesdir).

**Возвращает:**

`{Object}` - Копия объекта, экспортируемого файлом набора.
- `{SuiteOptions} [options]` - Дополнительные параметры объединения. См. выше.
___

#### `merge(...suites)`
Объединяет наборы тест-кейсов.

**Аргументы:**

- `{Object|HooksDeclaration} suites` - Наборы тест-кейсов.

**Возвращает:**

`{Object}` - Объединенный набор.

___

#### `makeCase(testCase)`
Создает тест-кейс с привязкой мета-тегов к тесту. Мета-теги сохраняются в свойстве `meta` объекта `test` и могут быть использованы для фильтрации запускаемых тестов, а так же в других компонентах.

**Аргументы:**

- `{CaseDeclaration} testCase` - Объект-декларация теста. Объект имеет единственное обязательное свойство `test` - функцию, реализующую тест. Остальные ключи не являются обязательными, но должны соответствовать разрешенным мета-тегам в параметре [`metaTags`](https://github.yandex-team.ru/market/hermione-suite-manager#array-metatags) конфигурации плагина.

**Возвращает:**

`{Function}` - Тело кейса, переданное в `testCase.test`.

**Пример:**

```js
const {makeCase} = require('@yandex-market/hermione-allure-reporter');

describe('Suite', () => {
    it('Case', makeCase({
        // Список мета-тегов
        id: '666',
        issue: 'MARKETFRONTEND-666',
        environment: 'prestable',
        severity: 'blocker',
        description: 'My Test Case',
        params: {name: 'My Param'},
        // Тест
        test() {
            return this.params.name.should.to.be.ok;
        }
    }));
});
```

___

#### `makeSuite(suiteName, suite)`
Создает съют с привязкой мета-тегов к внутренним тестам. При использовании фильтра тестов имеют больший приоритет, чем мета-теги внутренних тестов.

**Аргументы:**


- `{string} suiteName` - Имя съюта. Используется для формирования пути к тесту в отчетах Allure. 
- `{SuiteDeclaration} suite` - Объект-декларация съюта. Имеет одно обязательное свойство: `story` - объект-съют. Остальные ключи не являются обязательными, но должны соответствовать разрешенным мета-тегам в параметре [`metaTags`](https://github.yandex-team.ru/market/hermione-suite-manager#array-metatags) конфигурации плагина.

**Возвращает:**

`{Object}` - Съют, переданный в `suite.story`.

**Пример:**

```js
const {makeSuite} = require('@yandex-market/hermione-allure-reporter');

module.exports = makeSuite('Suite name', {
    feature: 'My Feature',
    environment: 'testing',
    story: {
        // Body of suite.
    }
})
```
