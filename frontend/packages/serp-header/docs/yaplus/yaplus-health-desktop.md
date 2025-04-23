## Блок `yaplus` на desktop
### Использование
```javascript
const dist = require('@yandex-lego/serp-header/dist/health/yaplus.desktop');

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
        /*  Ссылка на промо Плюса */
         yaplusUrl,

    }
    

});
```



### Разработка
Разработка ведётся в контрибе `contribs/serp-header`.
Чтобы собрать примеры блока нужно запустить:
`YENV=testing block=yaplus platform=desktop npm run build-examples`
Они соберутся в корне `islands` в `desktop.examples/yaplus`.
Можно увидеть их, запустив в корне `npx http-server` и открыв http://127.0.0.1:8080/desktop.examples/yaplus.
