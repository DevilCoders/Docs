## Блок `header3` на touch-phone
### Использование
```javascript
const dist = require('@yandex-lego/serp-header/dist/images/header3.touch-phone');

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

    
    /* Параметры, которые подставятся в разметку.
     *
     * Параметры вида (ctx.param === 1 ? 'hello' : 'world') - это выражения,
     * которые выполняются у нас внутри getContent() в момент его вызова.
     * То есть, тут нужно передавать `ctx: { param: 1 }`, например.
     */
    ctx: {
        /*  При сборке модификаторы заменяются на header3_scrolled_ + (...), а нам нужен модификатор true. */
         (ctx.scrollable ? "yes header3_scrolled" : "no" ),

    }
    

});
```



### Разработка
Разработка ведётся в контрибе `packages/serp-header`.
Чтобы собрать примеры блока нужно запустить:
`YENV=testing block=header3 platform=touch-phone npm run build:dev`
Они соберутся в корне `islands` в `touch-phone.examples/header3`.
Можно увидеть их, запустив в корне `npx http-server` и открыв http://127.0.0.1:8080/touch-phone.examples/header3.
