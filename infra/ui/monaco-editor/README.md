# Библиотека `@yandex-infracloud-ui/monaco-editor`

Компоненты monaco-editor и его производных.

```shell
npm i @yandex-infracloud-ui/monaco-editor
```

В вашем проекте должны быть установлены пакеты

```json
"peerDependencies": {
    "@yandex-data-ui/common": "^9",
    "@yandex-infracloud-ui/libs": "^0.2.10-beta.3",
    "monaco-editor": "^0.33.0"
}
```

## MonacoEditor

Обёртка для React для monaco-editor
![monaco editor](./docs/monaco-editor.png)

Используйте `LazyMonacoEditor`, чтобы не добавлять monaco-editor в бандл приложения.

Все свойства компонента можно посмотреть в типе `MonacoEditorProps`.

## YamlEditor

Редактор для yaml с поддержкой json-schema.
Реализует LazyMonacoEditor c поддержкой yaml через `monaco-yaml`.
![yaml editor](./docs/yaml-editor.png)

### Регистрация json схем

Импортируйте функцию `registerYamlJSONSchema`, далее с её помощью региструйте схемы или заменяйте существующие.

```js
registerYamlJSONSchema({
    schemaSettings: {
        // маска, по которой срабатывает схема; применяется к свойству schemaUri в YamlEditor
        fileMatch: ['*'],
        // встроенная схема, если отсутствует, будут скачана из uri
        schema: {
            type: 'object',
            properties: {
                deploy_units: {
                    type: 'object',
                    patternProperties: {
                        '.*': {
                            type: 'object',
                            properties: {
                                network_defaults: {
                                    type: 'object',
                                    description: 'Настройки сети',
                                },
                            },
                        },
                    },
                },
            },
        },
        // реальный uri схемы, либо при наличии schema любой uri по вашим соглашениям
        uri: 'https://deploy.yandex-team.ru/yp/stageSpec.json',
    },
});
```

### Поддержка для webpack плагина

Так как yaml через сторонний пакет отличается от встроенного в monaco, его необходимо добавить как кастомный язык

Сначала скачайте функцию для добавления языка

```js
const { addMonacoYaml } = require('@yandex-infracloud-ui/monaco-editor/build/cjs/services/addMonacoYaml');
```

Далее при использовании плагина `MonacoWebpackPlugin` необходимо добавить yaml в `customLanguages`:

```js
new MonacoWebpackPlugin({
    languages: [],
    features: [],
    customLanguages: [addMonacoYaml()], // <- здесь могут быть и другие языки
});
```

## Темизация

По умолчанию зарегистрированы и применяются две темы: светлая `infracloud-ui` и тёмная `infracloud-ui-dark`.
Темы подстраиваются под текущую тему common, но можно выставить и вручную.

## Цвета
Все цвета доступны в js через переменную `namedColors`, либо в css через css переменные с префиксом `--color-*`, например `--color-code-light-blue`.

Для темизации monaco нужны rgb значения цветов, поэтому при регистрации темы поверх существующих тем можно использовать доступные цвета в js. Для внешних элементов подойдёт css.

## Разработка
См. [CONTRIBUTING.md](./CONTRIBUTING.md)

## История версий
См. [CHANGELOG.md](./CHANGELOG.md)
