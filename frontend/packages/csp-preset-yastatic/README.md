# Пресет правил CSP для работы с yastatic.net

В состав входят следующие пресеты:
* script
* style
* font
* image
* frame
* connect
* media
* object
* worker

## Как пользоваться
```js
const expressYandexCSP = require('express-yandex-csp');
const yastaticCSP = require('csp-preset-yastatic');

app.use(expressYandexCSP({
    policies: myConfig.csp,
    presets: [
        yastaticCSP.script,
        yastaticCSP.style,
        yastaticCSP.frame
    ]
}));
```
