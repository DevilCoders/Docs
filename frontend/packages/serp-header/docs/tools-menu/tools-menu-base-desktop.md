## Блок `tools-menu` на desktop
### Использование
```javascript
const dist = require('@yandex-lego/serp-header/dist/base/tools-menu.desktop');

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


Клиентский JS этого блока можно подключать через `.getContent()`:
```javascript
const js = dist.getContent({ content: 'js' });
```
Но вообще он версионируется и выкладывается на статику. Чтоб подключать всегда актуальную версию можно сделать так:
```javascript
/* Заимпортить файл с данными о статике из корня пакета */
const staticData = require('@yandex-lego/serp-header/static.meta');
/* И сформировать путь до файлика с JS */
const scriptSrc = `${staticData.BASE_PATH}base/tools-menu/tools-menu-base.desktop.client.js`
```
Получится что-то вроде `https://yastatic.net/s3/frontend/@yandex-lego/serp-header/v0.43.0/base/notifier/notifier-base.desktop.client.js`, можно подключить это где-нибудь в конце страницы.


### Разработка
Разработка ведётся в контрибе `packages/serp-header`.
Чтобы собрать примеры блока нужно запустить:
`YENV=testing block=tools-menu platform=desktop npm run build:dev`
Они соберутся в корне `islands` в `desktop.examples/tools-menu`.
Можно увидеть их, запустив в корне `npx http-server` и открыв http://127.0.0.1:8080/desktop.examples/tools-menu.
