## Блок `yandex-header` на desktop
### Использование
```javascript
const dist = require('@yandex-lego/serp-header/dist/mail/yandex-header.desktop');

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
        /*  Цветовая тема шапки — default | white | black | grey, по умолчанию default */
         theme,

         /*  Ссылка на логотипе сервиса */
         serviceLogoUrl,

         /*  больше нигде не понадобится, можно унести в projects/mail */
         (ctx.customLogoImageUrl ? \`${this.reapply(apply('custom-logo-base'))}\` : \`${this.reapply(apply('logo-base'))}\`),

         /*  Ссылки в шапке: [{ href: 'yandex.ru', text: 'Main', active: true, shortText: 'M' }], но можно и HTML [{html: '<h1>Hello!</h1>'}] */
         nav,

         /*  Текст плейсхолдера в поисковой строке */
         inputPlaceholderText,

         /*  Максимальная длина для инпута в поисковой строке */
         inputMaxLength,

         /*  action поисковой формы */
         formAction,

         /*  Рендерить placeholder вместо формы поиска */
         searchPlaceholder,

         /*  eslint-disable-next-line quotes */
         tld,

         /*  Кнопка-ссылка, вставляется при наличии actionButtonText и actionButtonLink */
         actionButtonText,

         /*  Кнопка-ссылка, вставляется при наличии actionButtonText и actionButtonLink */
         actionButtonLink,

         /*  HTML Плюса, логика показа отдаётся сервису – если передали, рисуем, блок yaplus */
         yaplusHTML,

         /*   Иконка-ссылка Все сервисы @boolean */
         showAllServicesIcon,

         /*  HTML иконки Коллекций, блок favorites-icon */
         favoritesHTML,

         /*  HTML Колокола, вставляется только при наличии uid, блок notifier */
         notifierHTML,

         /*  Вставка Колокола */
         (ctx.uid && ctx.notifierHTML || ""),

         /*  HTML ссылки Регистрация, вставляется только если нет !uid, блок signup-link */
         signupHTML,

         /*  Вставляется контейнер-заглушка вместо блока пользователя */
         userPlaceholder,

         /*  HTML кнопки Войти, блок login-button */
         loginHTML,

         /*  HTML блока пользователя, блок user2 */
         userHTML,

         /*  В шапку вставляется кнопка Войти или Блок пользователя в зависимости от наличия uid в ctx */
         uid,

         /*  retpath */
         retpath,

         /*  Параметр origin в ссылке на Паспорт */
         origin,

         /*  Ссылка на все сервисы */
         allLink,

    }
    

});
```



### Разработка
Разработка ведётся в контрибе `packages/serp-header`.
Чтобы собрать примеры блока нужно запустить:
`YENV=testing block=yandex-header platform=desktop npm run build:dev`
Они соберутся в корне `islands` в `desktop.examples/yandex-header`.
Можно увидеть их, запустив в корне `npx http-server` и открыв http://127.0.0.1:8080/desktop.examples/yandex-header.
