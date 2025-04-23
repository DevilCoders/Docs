# useless-artifacts

Плагин для `gemini` и `hermione`, который по заданным маскам выводит в консоль список файлов, которые не использовались в прогоне тестов.

## Установка

```bash
$ npm install @yandex-int/useless-artifacts --registry=http://npm.yandex-team.ru
```

## Использование

### hermione

```js
module.exports = {
    plugins: {
        '@yandex-int/useless-artifacts/hermione': {
            enabled: true,
            patterns: [
                'features/**',
                'hermione/**'
            ]
        }
    }
};
```

### gemini

```js
module.exports = {
    system: {
        plugins: {
            '@yandex-int/useless-artifacts/gemini': {
                enabled: true,
                patterns: [
                    'features/**',
                    'gemini/**'
                ]
            }   
        }
    }
};
```
