# eslint-plugin-market

Проверяет специфичные для Маркета правила

## Установка

```
$ npm i eslint-plugin-market --save-dev
```


## Использованиe

Добавьте `market` в секцию плагинов в вашем `.eslintrc` файле. Можно опустить `eslint-plugin-` префикс:

```json
{
    "plugins": [
        "market"
    ]
}
```

Далее добавьте правила, которые вы хотите использовать в проекте:
```json
{
    "rules": {
        "market/ginny/no-compound-selector": "error",
        "market/ginny/no-page-object-service-locator": "error",
        "market/ginny/no-page-object-get": "error",
        "market/ginny/no-only-in-suitename": ["error", ["only", "omg"]],
        "market/ginny/no-synchronous-this-expect": "error",
        "market/ginny/no-use-deprecated-environments": ["error", ["all", "prestable"]],
        "market/ginny/no-use-forbidden-assertions": ["error", ["true", "false"]],
        "market/ginny/no-pause": "error",

        "market/mandrel/require-resolver-name": "error",

        "market/stout/no-service-locator": "error",

        "flow/suppress-comment": ["error", [{
            "suppress": "$FlowIgnore",
            "pattern": "MOBMARKET-\\d+"
        }, {
            "suppress": "$FlowFixMe",
            "pattern": "(MARKETVERSTKA|MOBMARKET|MARKETFRONTECH)-\\d+"
        }]],
        "flow/force-type-arguments": ["error", [{
            "name": "redux-actions",
            "functions": ["createAction"],
        }]],

        "market/apiary/no-context-manipulations": ["error", {
            "files": ["**/path/to/widgets/**/controller.js", "maybe/other/specific/path"],
            "contextArgumentName": ["ctx", "context"]
        }],

        "remote-widgets/neighbour-config": "error",

        "market/no-array-constructor-with-spread": "error",
        "market/no-global-moment-locale": "error",
        "market/no-spreading-set": "error",
    }
}
```

## Поддерживаемые правила

* [`ginny/no-compound-selector`](/docs/rules/ginny/no-compound-selector.md)
* [`ginny/no-skip`](/docs/rules/ginny/no-skip.md)
* [`ginny/no-page-object-service-locator`](/docs/rules/ginny/no-page-object-service-locator.md)
* [`ginny/no-only-in-suitename`](/docs/rules/ginny/no-only-in-suitename.md)
* [`ginny/no-page-object-get`](/docs/rules/ginny/no-page-object-get.md)
* [`ginny/no-synchronous-this-expect`](/docs/rules/ginny/no-synchronous-this-expect.md)
* [`ginny/no-use-deprecated-environments`](/docs/rules/ginny/no-use-deprecated-environments.md)
* [`ginny/no-use-forbidden-assertions`](/docs/rules/ginny/no-use-forbidden-assertions.md)
* [`ginny/no-pause`](/docs/rules/ginny/no-pause.md)
* [`ginny/no-import-suite`](/docs/rules/ginny/no-import-suite.md)
* [`mandrel/require-resolver-name`](/docs/rules/mandrel/require-resolver-name.md)
* [`stout/no-service-locator`](/docs/rules/stout/no-service-locator.md)
* [`flow/suppress-comment`](/docs/rules/flow/suppress-comment.md)
* [`flow/force-type-arguments`](/docs/rules/flow/force-type-arguments.md)
* [`apiary/no-context-manipulations`](/docs/rules/apiary/no-context-manipulations.md)
* [`i18n/static-keyset-name`](/docs/rules/i18n/static-keyset-name.md)
* [`remote-widgets/neighbour-config`](/docs/rules/remote-widgets/neighbour-config.md)
* [`no-array-constructor-with-spread`](/docs/rules/no-array-constructor-with-spread.md)
* [`no-global-moment-locale`](/docs/rules/no-global-moment-locale.md)
* [`no-spreading-set`](docs/rules/no-spreading-set.md)
* [`epics-expressions`](docs/rules/epics-expressions.md)
