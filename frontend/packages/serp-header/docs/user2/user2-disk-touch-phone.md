## Блок `user2` на touch-phone
### Использование
```javascript
const dist = require('@yandex-lego/serp-header/dist/disk/user2.touch-phone');

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
        /*  uid пользователя */
         uid,

         /*  yu пользователя */
         yu,

         /*  avatarId аватарки пользователя вида 0/0-0 */
         avatarId,

         /*  Имя пользователя */
         name,

         /*  URL редиректа после смены пользователя или выхода */
         retpath,

         /*  Обводка пользователей в Плюсе */
         hasPlus,

         /*  Ручка для получения списка аккаунтов, по умолчанию api.passport.yandex.{tld}/all_accounts */
         accountsUrl,

         /*  Показывать ли ссылку Получить Плюс */
         yaplusAvailable,

         /*  Кастомные элементы меню [{ text, url, action }] */
         customMenuItems,

         /*   Retpath в ссылке на залогин аккаунта. Используется вместе с флагом loggedByLink */
         loggedByLinkRetpath,

         /*  Флаг залогин аккаунтом из попапа юзера через get-запрос */
         loggedByLink,

         /*  Открывать ли попап по клику на текущего юзера */
         noUserPopup,

         /*  Ссылка для перехода по клику на текущего юзера (важно наличие свойства noUserPopup) */
         userClickLink,

         /*  Origin сервиса для кнопки выхода */
         logoutOrigin,

         /* center.yandex-team.ru\') + \'/api/v1/user/\' + (avatarId || \'0\') + \'/avatar/42.jpg\' : (ctx.avatarHost || \'https://avatars.mds.yandex.net\') + \'/get-yapic/\' + (avatarId || \'0/0-0\') + \'/islands-middle\' )}}_`}', */
         (ctx.isInternal ?  (ctx.avatarHost || \'https://center.yandex-team.ru\') + \'/api/v1/user/\' + (avatarId || \'0\') + \'/avatar/100.jpg\': (ctx.avatarHost || \'https://avatars.mds.yandex.net\') + \'/get-yapic/\' + (avatarId || \'0\') + \'/islands-retina-middle\' ),

         /*  поэтому если ее нет, камеру рисовать не нужно. */
         ((!ctx.avatarId || ctx.avatarId === '0/0-0') && (!ctx.isInternal || ctx.cameraUrl) ? \`${cam}\` : ''),

         /*  - готовим заранее html всех айтемов */
         ( ),

    }
    

});
```


Клиентский JS этого блока можно подключать через `.getContent()`:
```javascript
const js = dist.getContent({ content: 'js' });
```
Но вообще он версионируется и выкладывается на статику. Чтоб подключать всегда актуальную версию можно сделать так:
```javascript
/* Заимпортить файл с данными о статике из корня пакета */
const staticData = require('@yandex-lego/serp-header/static.meta');
/* И сформировать путь до файлика с JS */
const scriptSrc = `${staticData.BASE_PATH}disk/user2/user2-base.touch-phone.client.js`
```
Получится что-то вроде `https://yastatic.net/s3/frontend/@yandex-lego/serp-header/v0.43.0/base/notifier/notifier-base.desktop.client.js`, можно подключить это где-нибудь в конце страницы.


### Разработка
Разработка ведётся в контрибе `packages/serp-header`.
Чтобы собрать примеры блока нужно запустить:
`YENV=testing block=user2 platform=touch-phone npm run build:dev`
Они соберутся в корне `islands` в `touch-phone.examples/user2`.
Можно увидеть их, запустив в корне `npx http-server` и открыв http://127.0.0.1:8080/touch-phone.examples/user2.
