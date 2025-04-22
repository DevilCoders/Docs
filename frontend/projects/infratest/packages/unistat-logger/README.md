# unistat-logger

Плагин, позволяющий сохранять данные из unistat-ручки из report-renderer в json-файл после завершения работы templar-runner.

## Установка

```bash
npm install @yandex-int/unistat-logger --registry=http://npm.yandex-team.ru
```

## Использование

Параметры:

* `enabled` - включить / выключить плагин.
* `reportPath` - имя файла, куда будет сохраняться отчёт.

### Hermione

Подключить плагин в конфиге:

```js
module.exports = {
    plugins: {
        '@yandex-int/unistat-logger/hermione': {
            enabled: true,
            reportPath: 'renderer-unistat-report.json',
        }
    }
};
```

### Gemini

Подключить плагин в конфиге:

```js
module.exports = {
    plugins: {
        '@yandex-int/unistat-logger/gemini': {
            enabled: true,
            reportPath: 'renderer-unistat-report.json',
        }
    }
};
```
