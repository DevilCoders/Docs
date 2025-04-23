# Hermione-плагин для оценки тестового покрытия

**Предупреждение:** инструментирование с построением отчетов замедляет выполнение гермионы примерно на 50%

Для получения отчёта о покрытии необходимо:

1. Подключить плагин в конфиге гермионы.
```js
'@yandex-int/hermione-coverage': {
    enabled: Boolean(process.env.COVERAGE),
},
```
2. Собрать билд с плагином **babel-plugin-istanbul**.

Плагин `istanbul` должен идти последним в списке плагинов, иначе код может не собираться или могут возникать различные артефакты в собранном коде, которые сложно дебажить. 

Подключение через `babel-loader` и `webpack` (предпочтительно подключать этим способом):
```javascript
const { injectIstanbulPlugin } = require('@yandex-int/hermione-coverage/lib/helpers');

module.exports = {
    module: {
        rules: [
            {
                test: /\.ts$/,
                use: {
                    loader: 'babel-loader',
                    options: {
                        plugins: injectIstanbulPlugin(yourPlugins, yourConfig),
                    },
                },
            },
        ],
    },
}
```

При использовании `injectIstanbulPlugin` используется следующий дефолт для конфига плагина `istanbul`:
```javascript
{
    useInlineSourceMaps: true,
    include: [
        'src/**/*.ts',
        'src/**/*.tsx',
    ],
    exclude: [
        'src/**/*.test.ts',
        'src/**/*.test.tsx',
    ],
}
```

Подключение через конфиг `babel`:
```js
// babel.config.js
if (process.env.COVERAGE) {
    plugins.push('istanbul');
}
```
3. Запустить прогон тестов.

В корне проекта появится директория **__coverage** с HTML-отчётом и **__coverage-raw** с raw-отчетами.

## Получение покрытия с Report Renderer


**Внимание:** могут возникать ошибки при прогоне гермионы

Во время исполнения инструментированного **babel-plugin-istanbul** кода в RR, покрытие пишется в `global.__coverage__`.
Для того, чтобы это покрытие попало в отчёт, необходимо положить его в `window.__rrCoverage__` шаблона, который
возвращает RR.
Так как в `global.__coverage__` пишется покрытие о прогоне всех тестов, а не только текущего, необходимо в самом начале
функции `main` очищать `global.__coverage__` и передавать его значение в шаблон как можно позже, чтобы получить максимально полную информацию о покрытии.
Для этого плагин содержит две вспомогательные функции:
```js
// renderer.js
export function getMain(Util) {
    return function main(_, ctx) {
        if (process.env.COVERAGE) {
            require('@yandex-int/hermione-coverage/lib/helpers').clearRRCoverage();
        }

        // ...

        let rrCoverage;

        if (process.env.COVERAGE) {
            rrCoverage = require('@yandex-int/hermione-coverage/lib/helpers').getRRCoverage();
        }

        return getTemplate({
            ...data,
            rrCoverage,
        });
    };
}
```
```html
<!-- template.html -->
<% if (rrCoverage) { %>
<script>window.__rrCoverage__ = <%= rrCoverage %></script>
<% } %>
```
Или
```html
{{rrCoverage ? '<script nonce="' + nonce +'">window.__rrCoverage__ = ' + rrCoverage + '</script>' : ''}}
```

## Исключение файлов из покрытия

Исключить файлы из покрытия можно в опции **exclude** плагина **babel-plugin-istanbul**.

```js
if (process.env.COVERAGE) {
    plugins.push(['istanbul', {
        exclude: ['path/to/files'],
    }]);
}
```
