# @yandex-int/html-reporter-testpalm-plugin

Плагин для [html-reporter](https://github.com/gemini-testing/html-reporter) добавляющий новую кнопку в меню, которая помечает тегами тест-кейсы для всех упавших тестов и дает ссылку на них в TestPalm.

**Внимание!**
На данный момент плагин коректно работает лишь в CI, поэтому рекомендуется отключать его локально. Для этого можно воспользоваться переменной окружения `CI_SYSTEM` ([пример](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/.hermione.conf.js?rev=5d83cb62140d1b2a1e286fe2fc683d6e93079269#L32)).

## Требования

* `html-reporter@6.2.0`

## Установка

```bash
npm install @yandex-int/html-reporter-testpalm-plugin --save-dev --registry=https://npm.yandex-team.ru
```

## Использование

Добавьте следующую строчку к конфигу html-reporter:

```js
{
    pluginsEnabled: true,
    plugins: [
        {
            name: '@yandex-int/html-reporter-testpalm-plugin',
            component: 'TestPalmMenuItem',
            point: 'menu-bar',
            position: 'after',
            config: {
                testPalmProjectId: 'serp-js',
                projectName: 'web4',
            }
        }
    ]
}
```

## Опции конфигурации

### testPalmUrl

* Тип: `string`
* Значение по умолчанию: `https://testpalm.yandex-team.ru`

TestPalm URL.

### testPalmApiUrl

* Тип: `string`
* Значение по умолчанию: `https://testpalm-api.yandex-team.ru`

TestPalm API URL.

### testPalmProjectId

* Type: `string`

Id проекта в TestPalm.

### projectName

* Type: `string`

Название проекта (имя репозитория или сервиса в монорепозитории). Будет содержаться в теге.

### testComparator

* Type: `function`
* Значение по умолчанию:
    ```(js)
    function(testCase, hermioneTest) {
        return testCase.hermioneTitle === hermioneTest.testName;
    }
    ```

Функция, необходимая для того, чтобы соотнести упавшие тесты с тест-кейсами из Testpalm. Объект `testCase` содержит `id` и definitions, указанные в параметре `requiredDefinitions` в качестве ключей. Объект `hermioneTest` имеет следующую структуру:
```(json)
{
    "testName": "полное имя теста",
    "metaInfo": "объект с мета-информацией из отчета"
}
```

Если у вас на проекте используется [palmsync](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/palmsync) и вы не модифицируете имя тест-кейса с помощью [testCaseDecorator](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/palmsync/docs/configuration.md?rev=r8691043#testcasedecorator), то вам подойдет значение этой функции по умолчанию, иначе нужно будет явно соотносить автотест и тест-кейс.

### requiredDefinitions

* Type: `Array<string>`
* Значение по умолчанию: `['hermioneTitle']`

Список названий definitions из Testpalm, которые нужны для проведения соотвествия между автотестом из отчета и тест-кейсом из Testpalm.
