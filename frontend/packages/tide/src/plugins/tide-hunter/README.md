# tide-hunter

Плагин к tide для поиска дубликатов тестовых сценариев. 

## Конфигурация

Пример `tide.config.js` (указаны значения по-умолчанию):
```js
module.exports = {
    plugins: {
        'tide-hunter': {
            enabled: true,
            filePath: '.',
            urlCommands: ['url', 'yaOpenPage', 'yaOpenSerp'],
            index: null,
            minIndex: 0.9,
            maxIndex: 1,
            type: null,
            tool: 'hermione',
            diff: false,
            diffFilter: null,
            rules: {
                'same-url': {
                    enabled: true
                },
                'custom-before-rule': {
                    enabled: true,
                    hook: 'before',
                    matcher: (testData1, testData2, _, pluginConfig) => true,
                },
                'custom-after-rule': {
                    enabled: true,
                    hook: 'after',
                    matcher: (testData1, testData2, comparisonResult, pluginConfig) => true,
                },
            },
        },
        // ...
    },
};
```

## Использование

```
tide hunt [path] --type integration --tool hermione
```

- `[path]` — путь, внутри которого нужно искать тесты (defult: `'./'`).
- `-i, --index <number>` — индекс похожести тестов
- `--min, --min-index <number>` — минимальный индекс похожести тестов (default: `0.9`)
- `--max, --max-index <number>` — (default: `1`)
- `--type <string>` — тип, по которому будут отфильтрованы тесты (`integration`|`e2e`)
- `--tool <string>` — инструмент, по которому будут отфильтрованы тесты (`'testpalm'`|`'hermione'`, default: `'hermione'`, сравнение тестов происходит в рамках одной фичи, поэтому testpalm тесты читаются всегда, но могут не участвовать в сравнении)
- `--v-team <string>` — название команды, по которой будут отфильтрованы тесты
- `--feature <string>` — название фичи, по которому будут отфильтрованы тесты
- `--diff` — отображение диффа в спецификации тестов (default: `true`)
- `--same-url` — похожие тесты должны иметь тот же url (включает правило `'same-url'` для фильтрации тестов, default: `true`)
- `--same-platform` — похожие тесты должны иметь одинаковую платформу (включает правило `'same-platform'` для фильтрации тестов, default: `false`)
- `--diff-filter [string]` — похожие тесты должны включать данную подстроку в похожей части диффа (включает правило `'diff-filter'` для фильтрации тестов, default: `false`)
- `-h, --help` — вывод помощи
