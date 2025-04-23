# tide-testpalm-generator

Плагин к tide для автоматической генерации testpalm тестов. 
На данный момент доступна генерация `.testpalm.yml` файлов из `.hermione.js`. 

## Установка

```
npm install --save-dev @yandex-int/tide-testpalm-generator --registry=http://npm.yandex-team.ru
```

Чтобы включить плагин, необходимо указать его в конфиге tide.

## Использование

Плагин добавляет одну консольную команду:
```
tide generate /path/to/file [options]
```
`--ht, --hermione-to-testpalm` активирует режим генерации `hermione => testpalm`. По умолчанию включен.
`--rewrite` включает перезапись существующих тестов в целевом файле. По умолчанию включен.
`--no-rewrite` выключает перезапись существующих тестов в целевом файле.
`-A, --all-links` включает поиск testpalm файлов по всему проекту. По умолчанию выключен и поиск ведется только в одной директории с hermione файлом.

### Примеры использования

```
tide -c tide.config.js generate tests/test.hermione.js"
```

## Конфигурация

Пример `tide.config.js`:
```js
module.exports = {
    plugins: {
        '@yandex-int/tide-testpalm-generator': {
            enabled: true,
            replacers: {
                browser: {
                    assertView: args => ({ screenshot: `внешний вид [${args[0]}]` }),
                },                       
            },
        },
        // ...
    },
};
```

### `enabled: boolean`

Включает или отключает плагин. 

### `(optional) replacers: { [key: string]: any }`

Объект, задающий замены для функций в тестах. Можно определять замены в корне или на уровне конкретного объекта, например, `browser`.

Например, при конфигурации:
```js
{
    browser: {
        assertView: args => ({ screenshot: `внешний вид [${args[0]}]` }),
    }
}
```

Вызов `browser.assertView(arg)` будет преобразован в объект ``{ screenshot: `внешний вид [${args[0]}]` }``, который впоследствии будет преобразован к строке.
