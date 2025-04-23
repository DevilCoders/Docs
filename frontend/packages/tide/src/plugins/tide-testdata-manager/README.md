# tide-testdata-manager

Плагин к tide для автоматизации работы с дампами. 

Команда `update-url`, которую добавляет этот плагин, позволяет автоматически обновлять url во всех контекстах. 

## Установка
Чтобы включить плагин, необходимо указать его в конфиге tide.

## Использование
`npx tide update-url [searchPath] --old-url <query-string> --new-url <query-string>`
- `searchPath` - необязательный аргумент, позволяет задать путь, в котором нужно обрабатывать тесты
- `--old-url` и `--new-url` - опции, задающие старые и новые параметры url в формате query string или json-объекта.
Формат json-объекта соответствует формату, который возвращает `url.parse()`, но поле `query` представляется в виде entries:
```js
JSON.stringify({
    protocol: 'https:',
    host: 'example.com',
    query: [
        ['param-1', 'value-1']
    ]
    // ...
})
```

### Примеры использования
`npx tide update-url /some/path --old-url exp_flags=font_size=10 --new-url exp_flags=font_size=22`

С использованием json:

`npx tide update-url /some/path --old-url '{ "query": ["exp_flags", "font_size=10"] }' --new-url '{ "query": ["exp_flags", "font_size=22"] }'` 

## Конфигурация
Пример `tide.config.js`:
```js
module.exports = {
    plugins: {
        'tide-testdata-manager': {
            enabled: true,
            // ...
        },
        // ...
    },
};
```
### `enabled: boolean`
По умолчанию: `true`.

Включает или отключает плагин. 

### `commandNames: string[]`
По умолчанию: `[]`.

Массив имен команд в hermione тесте, в которых необходимо произвести замену.

### `urlUpdaters: UrlUpdaterFunction[]`
По умолчанию: `[hermioneReplacer, testpalmReplacer, testdataReplacer]`.

Массив функций, производящих модификации. Примеры реализации – см. `replacers.ts`.

### `searchPath: string`
По умолчанию: `.`.

Задает путь для поиска файлов.
