# Конфигурация

Конфигурация Palmsync возможна несколькими способами, в порядке повышения приоритета:

1. опции из конфигурационного файла `.palmsync.conf.js` ([подробнее](#конфигурация-с-помощью-файла-palmsyncconfjs));
1. опции команды в CLI ([подробнее](#конфигурация-с-помощью-опций-cli));
1. значения переменных окружения ([подробнее](#конфигурация-с-помощью-переменных-окружения)).

## Конфигурация с помощью файла `.palmsync.conf.js`

При запуске инструмент ищет файл `.palmsync.conf.js` в корне проекта.
Если такой файл отсутствует, то запуск Palmsync завершится с ошибкой.

Пример файла `.palmsync.conf.js`.

```js
module.exports = {
    validationOpts: {skip: ['tests']},
    synchronizationOpts: {skip: ['hermioneTests']},
    schemeExtension: [
        {
            name: 'v-team',
            required: true,
            meta: true,
            format: formats.isEnum(['team1', 'team2'])
        },
    ],
    filePatterns: {
        yaml: /\.yaml$/,
        hermione: /(hermione)\.js$/,
        hermioneE2e: /(hermione)\.js$/,
        tests: /(hermione|hermione\.e2e)\.js$/
    },
    sets: {
        hermione: {
            'desktop': {
                envs: [
                    {PLATFORM: 'desktop'}
                ]
            },
            'touch-pad': {...},
            'touch-phone': {...}
        },
        hermioneE2e: {
            'desktop': {
                envs: [
                    {PLATFORM: 'desktop'}
                ]
            },
            'touch-pad': {...},
            'touch-phone': {...}
        },
        yaml: {
            'desktop': {
                specs: ['features/common/**/*.yml', 'features/deskpad/**/*.yml', 'features/desktop/**/*.yml'],
                browsers: ['ie10', 'ie11', 'firefox', 'chrome-desktop'],
                envs: [
                    {PLATFORM: 'desktop'}
                ]
            },
            'touch-pad': {...},
            'touch-phone': {...}
        }
    },
    testCaseDecorator: (testCase) => {
        testCase.title += ' {{PLATFORM}}'; // к тайтлу каждого тестового сценария будет добавлена строка " {{PLATFORM}}"
        testCase.setField('platform', '{{PLATFORM}}') // закрепили за тестовым сценарием поле "platform" со значением "{{PLATFORM}}"
    },
    fullTitleComparator: (testCase, hermioneTestTitle) => {
        return testCase.fullTitle === hermioneTestTitle;
    },
    plugins: {
        'some-plugin': {
            param: 'value'
        }
    }
};
```

### validationOpts

Опции, используемые при валидации тестовых сценариев, расширяется опциями из CLI.

* `skip` – Отвечает за шаги валидации, которые нужно пропустить. Может принимать как одно, так и несколько значений. На данный момент доступны следующие значения:
    * `scenarios` — валидация тестовых сценариев будет пропущена.
    * `tests` — валидация тестов (`Hermione`) будет пропущена.

* `mode` – Режим в котором запущена валидация. Может принимать как одно, так и несколько значений. На данный момент доступны следующие значения:
    * `steps-group-syntax` – режим валидация синтаксиса [импортируемых шагов](./steps-group.md).
    * `automation-syntax` – режим валидации не автоматизированных сценариев. Проверяет наличие ключа **automation** в **specs** тест-кейса.
    * `soft-scenario-syntax` – в данном режиме валидатор не бросит исключение для файлов тестовых сценариев, содержащих синтаксические ошибки, и продолжит работу без использования невалидных файлов.
    * `required-tlds` – режим валидации полей [tlds](./yaml-files.md#tlds), по умолчанию данные поля не валидируются. Для работы требует наличие поля [requiredTlds](./configuration.md#requiredTlds).
    * `required-step-and-expect` – в данном режиме валидатор проверяет наличие в каждом тест-кейсе как минимум одного шага([do](./yaml-files.md#do)) и expect ([assert](./yaml-files.md#assert), [screenshot](./yaml-files.md#screenshot) или [tech](./yaml-files.md#tech)), по умолчанию не валидируется.
    * `required-step-before-expect` – в данном режиме валидатор проверяет, что перед каждой группой  expect ([assert](./yaml-files.md#assert), [screenshot](./yaml-files.md#screenshot) или [tech](./yaml-files.md#tech)) есть шаг([do](./yaml-files.md#do)), по умолчанию не валидируется.
    * `check-manual-scenario-screenshots` – в данном режиме валидатор проверяет, что ручные (не автоматизированные) тесты содержат скриншоты автотестов только с указанием [метки](./labels.md) (например, `[some-label >> some-screenshot]`)

Пример:

```js
{
    validationOpts: {
        skip: ['tests'],
        mode: ['required-tlds']
    }
}
```

### synchronizationOpts

Опции, используемые при синхронизации тестовых сценариев, расширяется опциями из CLI.

* `maxSoftErrorsThreshold` *(number)* – максимально допустимое количество [мягких ошибок при синхронизации](./synchronize.md#Ошибки-синхронизации). (По умолчанию: *0*)
* `saveAttributeValues` *(string[])* — список атрибутов тест-кейсов в TestPalm, значения которых будут сохраняться при каждой синхронизации, если в YAML-файле не определены эти атрибуты. По умолчанию значение `[]`.
    * Значение `[]` подразумевает, что все дополнительные атрибуты, выставленные у тест-кейса в TestPalm, но отсутствующие у тест-кейса в YAML-файле, будут удалены при синхронизации.
    * Значение `['attribute']` подразумевает сохранение **всех значений** атрибута с именем `attribute` при синхронизации. При условии, что у тест-кейса в YAML-файле не указано значение для этого атрибута.
* `supportStepsGroup` *(boolean)* – поддержка [импорта шагов](./steps-group.md) при синхронизации.
* `formatter` - поддержка разных форматтеров для тест-кейсов при синхронизации:
    * `default` - форматтер по умолчанию
    * `withExpectationSyntax` - форматтер для поддержки [expectation в синтаксисе](./expectation-syntax.md)
* `skip` – список действий, которые необходимо пропустить при синхронизации:
    * `palmsyncApi` – инициализация Palmsync API (только для debug режима)
    * `remoteTests` – получение всех тест-кейсов из проекта в TestPalm (только для debug режима)
    * `definitions` – получение всех definition из проекта в TestPalm (только для debug режима)
    * `hermioneTests` – чтение тестов с помощью конфигурации `hermione`
    * `hermioneE2eTests` – чтение тестов с помощью конфигурации `hermione-e2e`
    * `urlsByShowCounters` – скачивание ресурса со списком соотвествия счетчиков и урлов до фичи
    * `removeTestCases` – удаление тест-кейсов из проекта в TestPalm (при наличии опции удаление производиться не будет)

Опции управления содержимым тест-кейса:

* `attachBetaUrlToTestCasePreconditions` — прикреплять ссылку на стенд к описанию тест-кейса. По умолчанию включено.
* `attachBugFilterLinkToTestCasePreconditions` — прикреплять ссылку на фильтр в Трекере с багами по YAML-файлу тест-кейса к описанию тест-кейса. По умолчанию включено.
* `attachSkippedTestsToTestCaseDescription` — прикреплять скипнутые тесты к описанию тест-кейса. По умолчанию включено.
* `attachAutomationTasksToTestCaseDescription` — прикреплять тикеты на автоматизацию к описанию тест-кейса. По умолчанию включено.

При очистке проекта командой palmsync clean будут использовать только некоторые опции из synchronizationOpts

Опции, используемые при удалении тестовых сценариев, расширяется опциями из CLI.

* `skip` – список действий, которые необходимо пропустить при очистке:
    * `palmsyncApi` – инициализация Palmsync API (только для debug режима)
    * `remoteTests` – получение всех тест-кейсов из проекта в TestPalm (только для debug режима)
    * `definitions` – получение всех definition из проекта в TestPalm (только для debug режима)

Пример:

```js
{
    synchronizationOpts: {
        supportStepsGroup: true,
        skip: ['hermioneTests'],
    }
}
```

### filePatterns

Объект, содержащий маски тестовых файлов и тестовых сценариев. По умолчанию используются следующие значения:

* `/\.yml$/` – для файлов тестовых сценариев;
* `/(hermione)\.js$/` – для `Hermione` тестов.
* `/(hermione\.e2e)\.js$/` – для `Hermione-e2e` тестов.
* `/(hermione|hermione\.e2e)\.js$/` – для селективной валидации. Ограничение на типы файлов.

### project

Название проекта в сервисе TestPalm.

### schemeExtension

Список полей, расширяющих [общую схему проектов](../lib/config/common-scheme.js).

Допустимые свойства полей:

#### schemeExtension.name

**Обязательное**. Если одно и то же имя используется в `schemeExtension` и в общей схеме проектов, то будет использовано поле из `schemeExtension`

#### schemeExtension.required

Если `true`, поле должно присутствовать во всех тестовых сценариях. По умолчанию `false`. Значением может
быть функция, которая принимает на вход объект тестового сценария. Таким образом организована проверка зависимых
полей, например:

```js
[{
    name: 'specs',
    required: (scenario) => !scenario['specs-integration'],
},
{
    name: 'specs-integration',
    required: (scenario) => !scenario['specs'],
}]
```

`scenario` — объект тестового сценария. Например, тестовый сценарий

```yaml
some: value
specs:
  Here:
    Test:
      - field: value
```

будет представлен в виде:

```js
{
    some: "value",
    specs: {
        Here: {
            Test: [
                {field: "value"}
            ]
        }
    }
}
```

#### schemeExtension.defaultValue

Для необязательного поля можно задать значение по умолчанию. Если `schemeExtension.required` равно `false`, или не задано, то для отсутствующего поля будет использовано значение по умолчанию. Для обязательного поля данный параметр не имеет смысла и игнорируется, если будет по ошибке включён в описание поля.

Пример использования:

```js
[{
    name: 'files',
    required: false,
    defaultValue: [],
    meta: true,
    format: formats.isArrayOfStrings
}]
```

#### schemeExtension.format

Валидатор для проверки значения поля сценария. Одно из значений, экспортируемых в `palmsync.formats`.

Валидация применяется к полю по его имени. Поля валидируются во всех [местах](#schemeextensionscope) сценария.

Список доступных валидаторов:
* `any` — валидатор по умолчанию
* `isBoolean`
* `isString`
* `isArray` - этот валидатор работает аналогично функции JavaScript `Array.isArray`
* `isObject`
* `isStringOrArray`
* `isArrayOfStrings` - этот валидатор проверяет, что поле массив и каждый его элемент является строкой.
* `isArrayOfObjects`
* `isStringOrArrayOfStrings`
* `isEnum` — эта функция возвращает валидатор, например `isEnum('a', 'b', 'c')`
* `isArrayOfEnums` — эта функция возвращает валидатор, например `isArrayOfEnums('a', 'b', 'c')`
* `checkScreenshot`
* `checkCounter`
* `checkExample`
* `checkParams`
* `checkBrowsers`

Устаревшие валидаторы:
* ~~`isStringOrArrayOfStringsDeep`~~ - используйте `isStringOrArrayOfStrings`
* ~~`isStringDeep`~~ - используйте `isString`
  
##### checkBrowsers

Форматтер `checkBrowsers` умеет не только валидировать наличие указанных браузеров.
Он так же добавляет возможность пользоваться функциональностью [notFor](./yaml-files.md#browsers) и [браузерных групп](./yaml-files.md#browsers).
Для этого необходимо переопределить в схеме поле `browsers`:

```js
// Подключаем набор формматеров
const formats = require('@yandex-int/palmsync').formats;

module.exports = {
// Сам конфиг...

// Дополняем схему полей, переопределяя схему для browsers:
  schemeExtension: [
    {
      name: 'browsers',
      required: false,
      meta: true,
      // Первым аргументом идет набор всех возможных браузеров, вторым группы браузеров.
      format: formats.checkBrowsers([
        'chrome', 'firefox'
      ], {
        'android-browsers': ['andr-chrome', 'andr-firefox']
      })
    }
  ]
};
```

#### schemeExtension.meta

Если `true` и поле указано в тестовом сценарии, то оно будет добавлено в атрибуты `testcase` в TestPalm (в
интерфейсе отображается в `Keys`).

Запрещено устанавливать значение `meta: false` ключу, который есть в [стандартной схеме](../lib/config/common-scheme.js) и имеет значение `meta: true`.

#### schemeExtension.mergeable

Если установлено в `true`, то при вычислении значения поля будут сконкатенированы значения полей от
тест-кейса и всех его родителей вплоть до тестового сценария. Например, поле `tags` объявлено следующим образом:

```js
{
    name: 'tags',
    mergeable: true,
    ...
}
```

Тогда для следующего сценария:

```yaml
tags: suite
specs:
  Во траве ли:
    tags: трава
    В огороде:
      - tags:
        - огород
```

для тест-кейса поле `tags` примет значение `[suite, трава, огород]`.

Если `mergeable` равняется `false` или не установлено, то будет использовано самое вложенное значение поля. В
приведённом примере поле `tags` будет равно `[огород]`.

#### schemeExtension.scope

Массив, в котором описаны допустимые места сценария, где может быть описано поле. Используется при [валидации](validation.md#проверка-структуры-сценария). 

Допустимые значения (обязательно импортировать как в примере ниже): `ROOT`, `TESTCASE`, `TESTGROUP`, `HOOK`. 

Если `scope` отсутствует, то по умолчанию считается, что поле может находиться в любом месте сценария.

```js
const {ROOT} = require('@yandex-int/palmsync').scopes

module.exports = {
    schemeExtension: {
        name: 'files',
        required: true,
        meta: true,
        format: formats.isArrayOfStrings,
        scope: [ROOT]
    }
}
```

#### schemeExtension.grammar

Набор правил для проверки опечаток. Например, поле `tags` в общей схеме объявлено следующим образом:

```js
{
    name: 'tags',
    grammar: [
        {reference: 'no_assessors', mask: /no[_-]?a[cs]{1,2}ess?ors?/}
    ],
    ...
}
```

Проверка применяется к вычисленному значению поля (с учётом флага `mergeable`). Если вычисленное значение поля —
массив, то проверка применяется к каждому элементу массива.

При проверке грамматики каждое значение, которое соответствует `mask`, но не равняется `reference`, сгенерирует
ошибку.

##### schemeExtension.reveal, schemeExtension.child

**Поля должны быть указаны вместе**. Включает особое поведение, при котором в схему проекта
динамически добавляются новые поля. Например, в общей схеме поле `params` объявлено следующим образом:

```js
{
    name: 'params',
    format: checkParams,
    reveal: true,
    child: {
        meta: true,
        mergeable: true
    }
}
```

Рассмотрим следующий сценарий:

```yaml
params:
  exp_flags: some_flag=1
specs:
  Тест:
    - params:
        foreverdata: 100500
        exp_flags: other_flag=2
```

Для этого сценария результат будет эквивалентен применению схемы:

```js
{
    name: 'params',
    format: checkParams,
},
{
    name: 'params.exp_flags',
    meta: true,
    mergeable: true
},
{
    name: 'params.foreverdata',
    meta: true,
    mergeable: true
}
```

к сценарию:

```yaml
params:
  exp_flags: some_flag=1
params.exp_flags: some_flag=1
specs:
  Тест:
    - params:
        foreverdata: 100500
        exp_flags: other_flag=2
    - params.foreverdata: 100500
    - params.exp_flags: other_flag=2
```

Для автосгенерированных полей устанавливаются свойства, перечисленные в `child`, но не наследуются свойства
оригинального поля.

В тестовых сценариях и тест-кейсах поле, использующее эту возможность, должно быть объектом.

**Все поля со значением `meta: true` будут автоматически добавлены в definitions в TestPalm.**

### paramsKeys

Массив ключей, допустимых к использованию в [`params`](yaml-files.md#params). Если параметр `paramsKeys` не объявлен или ему присвоен пустой массив, то проверка не применяется и множество ключей не ограничено.

Пример:

При валидировании сценария:

```yml
specs:
    Тест:
        - params:
            foreverdata: 100500
            expflags: some_flag=1 # опечатка в ключе
        - do: anything
        - assert: something
```

с такой конфигурацией:

```js
// palmsync.conf.js
module.exports = {
    paramsKeys: ['foreverdata', 'exp_flags']
}
```

валидация завершится с ошибкой, так как `expflags` не описан в `paramsKeys` и скорее всего является опечаткой.

### apiPath

Описание параметра в пакете [testpalm-api](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/testpalm-api#список-параметров-соединения). По умолчанию пустая строка.

### apiVersion

Описание параметра в пакете [testpalm-api](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/testpalm-api#список-параметров-соединения). По умолчанию `2`.

### hostname

Описание параметра в пакете [testpalm-api](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/testpalm-api#список-параметров-соединения). По умолчанию `testpalm-api.yandex-team.ru`

### chunkSizeOfBulkPush

Размер пачки тест-кейсов, которая отправляется в batch-ручку. По умолчанию `200`.

### chunkSizeOfTestCasesFetch

Количество запрашиваемых тест-кейсов для одного вызова ручки получения тест-кейсов. По умолчанию `1000`.

### testpalmToken

[Токен OAuth аутентификации](https://wiki.yandex-team.ru/testpalm/testpalmdoc/api/) для доступа к сервису TestPalm.

### concurrency

Количество одновременно выполняемых вызовов к API TestPalm. По умолчанию `5`.

### retries

Максимальное количество допустимых попыток для одного запроса. По умолчанию `8`.

### timeout

Максимально допустимое время выполнения запроса (в миллисекундах).

### retry

Настройки ретраев TestpalmAPI ([подробнее](https://github.yandex-team.ru/search-interfaces/ci/tree/master/packages/requests#описание-работы-ретраев))

По умолчанию:

```js
{
    maxRetryAfter: 300000 // 5 миинут
}
```

### hermioneConfigPath

Путь к конфигу для чтения `hermione`-тестов при валидации и синхронизации. Необязательная опция. В случае отсутствия, валидация и синхронизация для `hermione` не будут запущены.

### hermioneE2eConfigPath

Путь к конфигу для чтения `hermione-e2e`-тестов при валидации и синхронизации. Необязательная опция. В случае отсутствия, валидация и синхронизация для `hermione-e2e` не будут запущены.

### excludes

Экслюды для `hermione`, `hermione-e2e.`

По умолчанию:

```js
{
    hermione: [],
    hermioneE2e: []
}
```

### sets

Настройки, от которых зависит чтение файлов тестов (`Hermione`) и сценариев (пример использования выше).

Объект содержит описания сетов, обычно сет соответствует [платформе](./yaml-files.md#поддерживаемые-платформы). Каждый сет представляет собой объект с полями `envs`, `specs`, `baseUrl` и `browsers`.

#### sets.envs

Поле `envs` содержит переменные среды окружения, от которых зависит чтение файлов с тестами и сценариями. Также указанные
переменные будут являться значениями для подстановки плейсхолдеров в сценариях.

#### sets.specs

Поле `specs` — массив с масками для поиска файлов тестовых сценариев, относящихся к данному сету.
Более подробно про формат файловых масок можно прочитать [здесь](https://github.com/isaacs/minimatch).

#### sets.ignoreFiles

Поле `ignoreFiles` — массив с масками, исключающими директории из чтения.

> :book: Полезно в том случае, если паттерны, указанные в поле `specs`, написаны обобщённо и могут привести к чтению большого числа вложенных директорий. Например, `features/**/*.yaml`, когда в директории `features` есть множество вложенных директорий, которые не могут включать в себя YAML-файлы по правилам проекта.

#### sets.baseUrl

Поле `baseUrl` — содержит url беты с конкретной платформой. Если адрес относительный, то объединяется с корневым [baseUrl](#baseUrl).

#### sets.browsers

Поле `browsers` — это массив текстовых идентификаторов браузеров.

### baseUrl

Поле `baseUrl` – содержит url с бетой проекта.

### testCaseDecorator

Функция, позволяющая сконфигурировать декорацию каждого тестового сценария (пример использования выше).

### fullTitleComparator

Функция, позволяющая сконфигурировать способ сравнения фултайтлов тестовых сценариев и фултайтлов
`Hermione`-тестов (пример выше демонстрирует правило сравнения фултайтлов по умолчанию).

### plugins

Объект с плагинами, которые будут загружены с указанными опциями. Подробнее [здесь](./plugins.md#плагины).

### documentationLink

Ссылка на документацию, которая будет выведена при падении валидации тестовых сценариев.

По умолчанию https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync/README.md

### requiredTlds

Список разрешенных доменов верхнего уровня ([tlds](./yaml-files.md#tlds)), которые можно указать для каждого тест-кейса.

### scenarioTypes

Поддерживаемые типы сценариев. По умолчанию `specs` и `specs-integration`.
Данная опция указывает Palmsync откуда читать тест-кейсы в сценариях.

[Доступные типы сценариев](./yaml-fiels.md#Типы-сценариев).

### s3MdsUpload

Включает выгрузку скриншотов в S3 и подмену ссылок на них в шагах. По умолчанию выгрузка отключена. [Подробнее](./screenshots-upload.md) про настройку выгрузки скриншотов.

Требует указания бакета в S3 (см. [`s3MdsBucketName`](#s3MdsBucketName)).

### s3MdsEndpointUrl

S3 REST API. По умолчанию `https://s3.mds.yandex.net`.

### s3MdsPublicUrl

URL публичного API. По умолчанию `https://s3.yandex.net`.

### s3MdsBucketName

Название бакета в S3.

Бакет должен быть открыт наружу, если вы хотите раздавать задания асессорам или толокерам.

По умолчанию указан бакет `crowdtest`, доступный наружу. Завести свой бакет можно по [инструкции](https://wiki.yandex-team.ru/mds/s3-api/faq/#kakmnenachatpolzovatsjas3-apimds).

### s3MdsUploadJingScreenshots

Включает выгрузку скриншотов из jing в S3. По умолчанию `true`.

### calcEstimatedTime

Контролирует автоматический расчёт затраченного времени на тест-кейс. По умолчанию включено (`true`).

Подробнее про [расчет затраченного времени](./synchronize.md#Блок-с-расчетным-временем).

### assertActionCostInSecs

Стоимость шага `assert` в секундах, которое будет установлено всем тест-кейсам независимо от платформы.
По умолчанию: 20 секунд.

Подробнее про [расчет затраченного времени](./synchronize.md#Блок-с-расчетным-временем).

### screenshotActionCostInSecs

Стоимость шагов со скриншотами `assert` и `screenshot` в секундах, которое будет установлено всем тест-кейсам независимо от платформы.
По умолчанию: 20 секунд.

Подробнее про [расчет затраченного времени](./synchronize.md#Блок-с-расчетным-временем).

### strictLabels

Строгий режим проверки меток. В этом режиме допускается использовать только метки, объявленные в текущем файле, а также метки, объявленные в файлах, которые заданы в поле `import-labels`. [Подробнее](./labels.md)
По умолчанию: false.

## Конфигурация с помощью опций CLI

При вызове команд можно переопределить параметры конфигурации:
* `-p` или `--project`. Название проекта в сервисе TestPalm.
* `-c` или `--concurrency`. Количество одновременно выполняемых вызовов к API TestPalm.
* `-t` или `--timeout`. Максимально допустимое время выполнения запроса (в миллисекундах).
* `-r` или `--retries`. Максимальное количество допустимых попыток для одного запроса.
* `-d` или `--dry`. Флаг, который включает режим тестового запуска. При этом, все запросы, изменяющие данные в
TestPalm, не будут выполнять обращения к сервису, а только выводить соответствующие сообщения в консоль.
* `-s` или `--skip`. Подробное описание параметра [здесь](#validationOpts).
* `--s3-mds-upload`. Включает выгрузку скриншотов в S3 и подмену ссылок на них в шагах. По умолчанию выгрузка отключена.
* `--s3-mds-endpoint-url`. S3 REST API.
* `--s3-mds-public-url`. URL публичного API.
* `--s3-mds-bucket-name`. Название S3-контейнера.
* `--s3-mds-access-key-id`.
* `--s3-mds-access-secret-key`.
* `--chunk-size-of-bulk-push`. Размер пачки тест-кейсов, которая отправляется в batch-ручку.
* `--chunk-size-of-test-cases-fetch`. Количество запрашиваемых тест-кейсов для одного вызова ручки получения тест-кейсов.

## Конфигурация с помощью переменных окружения

Palmsync даёт возможность переопределять параметры, заданные в конфигурационном файле, с помощью переменных окружения.
Такие переменные должны иметь префикс `palmsync_` и совпадать по названию с опциями.

Например, для параметра `project`, соответствующая переменная окружения будет `palmsync_project`.
