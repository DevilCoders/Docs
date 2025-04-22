# html-reporter-dumps-plugin

Плагин для [hermione](https://github.com/gemini-testing/hermione) и [html-reporter](https://github.com/gemini-testing/html-reporter), отображающий информацию об используемых дампах (содержат данные с ответом на пользовательский запрос), которые сохраняет dev-сервер (например, [kotik](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/kotik)).

Так же плагин добавляет в hermione следующие cli-команды:
- `remove-unused-dumps` - команда для удаления неиспользуемых дампов (подробнее о использовании [ниже](#remove-unused-dumps));

## Требования:

- @yandex-int/kotik@2.9.0 (может работать и с другими dev-серверами, если отправлять данные в необходимом формате по шине данных)
- hermione@4.7.0
- html-reporter@7.7.1 (для работы cli команды `remove-unused-dumps` требуется html-reporter@8.4.0)

## Установка

```bash
npm install @yandex-int/html-reporter-testpalm-plugin --save-dev --registry=https://npm.yandex-team.ru
```

## Использование

### hermione

Необходимо подключить плагин в конфиге `hermione`:

```js
// .hermione.conf.js
module.exports = {
    // ...
    plugins: {
        // ...
        '@yandex-int/html-reporter-dumps-plugin/hermione': {
            enabled: true
        }
    }
};
```

Здесь:

* *enabled* (optional, `Boolean`) - включить/выключить плагин. По умолчанию плагин включен.

#### Что делает плагин

Плагин по шине межпроцессного взаимодействия ([ipbus](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/ipbus)) подписывается на топик `dumps-cache-info` и получает сообщения имеющие следующий формат:
```ts
{
    testRunId: string; // уникальный id теста
    cacheFile: string; // путь к дампу на файловой системе
    cacheKey: string; // ключ, на основе которого было сгенерировано имя дампа (обычно ключом является урл)
}
```

Где:

* *testRunId* (required, `String`) - уникальный id теста, необходим для матчинга запущенного теста с прочитанным дампом. Данный id генерит плагин [url-decorator](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/url-decorator);
* *cacheFile* (required, `String`) - путь к дампу на файловой системе, необходим, чтобы считать дамп и определить его состояние. Т.е. понять был ли дамп создан в ходе выполнения тестов, использовался ли при запуске или же был перезаписан и т.д;
* *cacheKey* (optional, `String`) - ключ, на основе которого было сгенерировано имя файла дампа. Обычно в качестве `cacheKey` используется url запроса. Так как имя файла дампа хешируется, то по нему невозможно понять какому дампу какой ключ соответствует. Соответственно, данное поле служит для матчинга между `cacheFile` и `cacheKey`.

Данные в таком формате должен отправлять dev-сервер. В [kotik](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/kotik) за это отвечает мидлвара [`cacheInfo`](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/kotik#cacheinfo).
Всю полученную информацию плагин сохраняет в своей таблице `dumps` в БД sqlite плагина [html-reporter](https://github.com/gemini-testing/html-reporter).

### html-reporter

Необходимо подключить плагин в конфиге `html-reporter`:

```js
// .hermione.conf.js
const htmlReporterDumpsPluginMount = require("@yandex-int/html-reporter-dumps-plugin/mount");

module.exports = {
    // ...
    plugins: {
        // ...
        'html-reporter/hermione': {
            enabled: true,
            pluginsEnabled: true,
            plugins: [
                // ....
                htmlReporterDumpsPluginMount()
            ]
        }
    }
};
```

#### Компоненты

##### DumpsInfo

Компонент отображает информацию о считанных дампах для каждого результата прогона тестов.

## CLI-команды

### remove-unused-dumps

Данная команда очищает проект от всех неиспользуемых дампов. Удаление происходит в два этапа:
- удаление дампов для которых тест отсутствет на файловой система;
- удаление дампов, которые не использовались в успешно выполненном тесте (результат тестов берется из базы данных [html-reporter](https://github.com/gemini-testing/html-reporter)). Для корректного выполнения html-отчет должен существовать на файловой системе и содержать результат прогона тестов. Желательно использовать отчет из CI.

Опции командной строки: `npx hermione remove-unused-dumps --help`

```
  Usage: remove-unused-dumps [options]

  remove dumps which were not used when running tests

  Options:

    -p, --pattern <pattern>  pattern for searching dumps on the file system
    --skip-questions         do not ask questions during execution (default values will be used)
    -h, --help               output usage information

  Example of usage:
    Specify the folder in which all dumps are located:
    npx hermione remove-unused-dumps -p hermione-dumps-folder

    Specify the mask by which all dumps will be found:
    npx hermione remove-unused-dumps -p 'test-data/**/*.json.gz'

    Specify few masks by which all dumps will be found:
    npx hermione remove-unused-dumps -p 'test-data/**/chrome/*.json.gz' -p 'test-data/**/firefox/*.json.gz'

    Don't ask me about anything and just delete unused dumps:
    npx hermione remove-unused-dumps -p 'hermione-dumps-folder' --skip-questions
```
