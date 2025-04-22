## Блок `signup-link` на touch-phone
### Использование
```javascript
const dist = require('@yandex-lego/serp-header/dist/weather/signup-link.touch-phone');

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
Разработка ведётся в контрибе `contribs/serp-header`.
Чтобы собрать примеры блока нужно запустить:
`YENV=testing block=signup-link platform=touch-phone npm run build-examples`
Они соберутся в корне `islands` в `touch-phone.examples/signup-link`.
Можно увидеть их, запустив в корне `npx http-server` и открыв http://127.0.0.1:8080/touch-phone.examples/signup-link.
