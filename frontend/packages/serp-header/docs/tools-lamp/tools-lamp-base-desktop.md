## Блок `tools-lamp` на desktop
### Использование
```javascript
const dist = require('@yandex-lego/serp-header/dist/base/tools-lamp.desktop');

const content = dist.getContent({
    /* идентификатор бандла (base по умолчанию) */
    key: 'base',

    /* домен */
    tld: 'ru',

    /* язык */
    lang: 'ru',

    /* массив экспериментальных флагов, если есть эксперименты с этим блоком */
    expFlags: [{ flagName: flagValue }],

    /*
     * Тип возвращаемого контента.
     * Тут html, css или js, all – это html + css
     */
    content: 'all',

    /* nonce */
    nonce: 123,

    

});
```



### Разработка
Разработка ведётся в контрибе `packages/serp-header`.
Чтобы собрать примеры блока нужно запустить:
`YENV=testing block=tools-lamp platform=desktop npm run build:dev`
Они соберутся в корне `islands` в `desktop.examples/tools-lamp`.
Можно увидеть их, запустив в корне `npx http-server` и открыв http://127.0.0.1:8080/desktop.examples/tools-lamp.
