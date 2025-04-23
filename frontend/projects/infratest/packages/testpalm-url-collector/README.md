# testpalm-url-collector

Плагин для [palmsync](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/palmsync), предназначен для сбора урлов из тестовых сценариев при синхронизации.
Результатом работы плагина являются `json`-отчеты, в которых собраны урлы тестовых сценариев по платформам:
```json
[
    {"path":"https://some.yandex.beta/search/?some=query"},
    {"path":"https://some.yandex.beta/search/?other=query"}
]
```

## Подключение

Для подключения данного плагина, необходимо указать его в конфигурационном файле `palmsync`:

```js
// palmsync.conf.js
// ...
plugins: {
    '@yandex-int/testpalm-url-collector': {
        reportDir: 'some/path'
    }
}
// ...
```
где:
* `enabled` **[Boolean]** - отвечает за включение плагина, `true` по умолчанию.

* `reportDir` **[String]**: - путь к директории, в которой будут сохранены отчеты, `testpalm-urls` по умолчанию.
