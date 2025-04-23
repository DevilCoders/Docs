# Пакет с общими мидлварами/пресетами/хелперами для работы с `@yandex-int/frontend-kotik`

Пакет находится в разработке, постоянно будут добавляться новые мидлвары/пресеты/хелперы.
Если вы не нашли нужного вам функционала в пакете, пожалуйста, не стесняйтесь, делайте pr.

## Оглавление

- [Пресет для работы с webpack `frontend-webpack-preset`](#пресет-для-работы-с-webpack-frontend-webpack-preset)
- [Мидлвар для установки имени файла дампа `cacheFilename`](#мидлвар-для-установки-имени-файла-дампа-cachefilename)
- [Пресет для работы с json-форматом данных `frontend-json-preset`](#пресет-для-работы-с-json-форматом-данных-frontend-json-preset)
- [Пресет для замены картинок на "шахматку" `frontend-image-proxy`](#пресет-для-замены-картинок-на-шахматку-frontend-image-proxy)
- [Утилита для создания роутов-редиректов `utils/redirect.js`](#утилита-для-создания-роутов-редиректов-utilsredirectjs)

---

### Пресет для работы с webpack `frontend-webpack-preset`

Несколько мидлваров, которые в момент старта котика запустят вебпак, плюс автоматический soft-рестарт котика при изменении серверного шаблона.

##### Как использовать

Достаточно просто подключить пресет к общему пулу мидлваров в нужном роуте:

```js
'use strict';

const { presets } = require('@yandex-int/archon-renderer-devserver-command');
const frontendPresets = require('@yandex-int/frontend-kotik');

module.exports = {
    routes: [
        {
            matcher: ({ kotik: { parsedURL: { pathname } } }) => pathname.startsWith('/profile'),
            handler: presets['serp-apphost-frontend-dynamic'] // дефолтный пресет для работы с аппхостовыми данными
                .addFirst(frontendPresets['frontend-webpack-preset'].middlewares), // подключаем пресет с вебпак мидллварами
            context: {
                source: {
                    hostname: 'hamster.yandex.ru',
                    protocol: 'https',
                    searchParams: {
                        renderer_export: 'binary'
                    }
                }
            }
        }
    ]
};

```

В данный момент пресет не имеет настроек, и работает сразу и с клиентским, и с серверным бандлом вебпака, ожидается, что конфиги вепбака будут лежать в вашем проекте по адресу `.config/webpack/client` и `.config/webpack/server`.
Если для вашего проекта такое поведение не подходит, смело делайте pr с возможностью прокинуть какие-либо настройки.


---

### Мидлвар для установки имени файла дампа `cacheFilename`

Мидлвар для простановки в контекст котика переменной `cacheFilename`, которая используется в других мидлварах для работы с дампами.

##### Как использовать

Необходимо импортнуть creator мидлвара по пути `@yandex-int/frontend-kotik/middlewares/cache-filename` и вызвать creator для создания мидлвара.

Creator принимает в себя один аргумент `paramsToRemove` – это массив с названием query-параметров, которые НЕ будут участвовать/влиять на хэш дампа.
У этого параметра есть дефолтное значение `defaultParamsToRemove = ['reqid', 'suggest_reqid', 'tpid', 'rnd', 'testRunId', 'session_info', 'st', 'yu'];`

```js
'use strict';

const { presets } = require('@yandex-int/archon-renderer-devserver-command');
const { cacheFilenameMiddleware, cacheFilename } = require('@yandex-int/frontend-kotik/middlewares/cache-filename');

module.exports = {
    routes: [
        {
            matcher: ({ kotik: { parsedURL: { pathname } } }) => pathname.startsWith('/static') || pathname.startsWith('/_'),
            handler: presets['serp-apphost-frontend-static']
        },
        {
            matcher: ({ kotik: { parsedURL: { pathname } } }) => pathname.startsWith('/profile'),
            handler: presets['serp-apphost-frontend-dynamic']
                .addFirst(cacheFilenameMiddleware()) // можно без аргументов
                .addFirst(cacheFilenameMiddleware(['someKey', 'anotherKey'])) // можно передать свой массив
                .addFirst(cacheFilenameMiddleware(cacheFilename.defaultParamsToRemove.concat('myKey')))  // можно расширить/урезать дефолтные параметры
            context: {
                source: {
                    hostname: 'hamster.yandex.ru',
                    protocol: 'https',
                    searchParams: {
                        renderer_export: 'binary'
                    }
                }
            }
        }
    ]
};
```
---
### Пресет для замены картинок на шахматку `frontend-image-proxy`

То же самое, что и в web4 под темпларом, только в котике. Ищет в зарендеренных кусках html/json ссылки на картинки и заменяет их 'шахматкой'.
Есть возможность выбора регулярками конкретных изображений для замены 'шахматкой' (см. описание конфига).
Мидлвара будет работать только когда указан параметр `cacheMode` (--play, --save, --create).

Сама шахматка генерируется пакетом [@yandex-int/gemini-serp-stubs](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/gemini-serp-stubs).
Дефолтные хосты и параметры для генерации 'шахматки' перечислены [тут](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/frontend-kotik/middlewares/image-proxy/utils/constants.js).
Одна и та же картинка на странице будет заменена одинаковой 'шахматкой', однако на разных страницах есть вероятность того,
что 'шахматка' для одной и той же картинки будет разной, это связано с тем, что, чтобы узнать исходный размер картинки, за ней отправляется запрос, он может упасть по таймауту, тогда размеры 'шахматки' будут регламентированы дефолтными значениями.  При работе с `cacheMode`-параметром `--play`, размеры картинок будут взяты из контекста, запросы за оригинальными картинками отправлены не будут.

В дефолтном режиме работы картинки будут подменяться на инлайновые стабы 'шахматок', в случае, если такое поведение не устраивает, можно явно запретить инлайнить стабы параметром `hermione_disable_image_proxy_inline_stubs=1`. В этом случае будут генерироваться урлы типа `/images?width=10...`.
С помощью конфига возможно настроить урлы, по которым будут генерироваться неинлайновые 'шахматки'  (см. `proxyPath` в конфиге).

##### Как использовать

Импортировать утилиту, добавить конфиг (при необходимости), добавить роуты для генерации неинлайновых 'шахматок',
добавить мидлвары в конфиг котика в любое место после отрабатывания стандартной котиковской мидлвары
 [render](https://github.yandex-team.ru/search-interfaces/infratest/blob/e947a23b6dcd453bf8fd31dffb5b0961fa6ca7ba/packages/kotik/middleware/render.js), которая поставляется в стандартном пакете `@yandex-int/archon-renderer-devserver-command`.

```js
const frontendPresets = require('@yandex-int/frontend-kotik');
const imageProxyConfig = {
    // Хосты добавятся к дефолтным и будут учитываться при поиске картинок
    hosts: ['image.com'],
    // Все найденные картинки, удовлетворяющие хостам будут профильтрованы через описанный набор регулярок
    filterRegExps: [/doctor_104/],
    // Урлы для генерации неинлайновой 'шахматки'
    proxyUrls: {
        // урл для 'шахматки' favicon-ок, которые были запрошены с хоста favicon.yandex.net
        favicon: '/favicon-generator',
        // урл для всех остальных 'шахматок'
        image: '/image'
    }
}
const { routes: imageProxyRoutes, middlewares: imageProxyMiddlewares } = frontendPresets['frontend-image-proxy'](imageProxyConfig);

module.exports = {
    routes: [
         ...imageProxyRoutes,
        {
            matcher: ({ kotik: { parsedURL: { pathname } } }) =>
                pathname.startsWith('/static') || pathname.startsWith('/_'),
            handler: presets['serp-apphost-frontend-static'],
        },
        {
            matcher: ({ kotik: { parsedURL: { pathname } } }) => pathname.startsWith('/health'),
            handler: presets['serp-apphost-frontend-dynamic']
                    // Можно после любой миделвары, идущей сразу или после 'render'
                    .addAfter('render', imageProxyMiddlewares),
            context: {
                source: {
                    hostname: 'hamster.yandex.ru',
                    protocol: 'https',
                    searchParams: {
                        renderer_export: 'binary',
                        renderer_render_on_export: '1',
                    },
                },
            },
        },
    ],
};

```

---

### Мидлвар для добавления экспериментальных флагов

Для апхоста есть [источник экспериментов](../frontend-apphost-context/src/sources/experiments.ts), который предоставляет данные об экспериментальных флагах, включенных для запроса.

В тестах необходимо уметь устанавливать флаги. Этот мидлвар устанавливает флаги из query-параметра `expFlags` в поле `flags` источника `experiments`.

Мидлвар не изменяет данные, записываемые в дамп. Он добавляет новые флаги после чтения дампов или получения данных от бэкенда.

##### Как использовать

Необходимо импортнуть creator мидлвара по пути `@yandex-int/frontend-kotik/middlewares/append-exp-flags` и вызвать creator для создания мидлвара.

```js
'use strict';

const { presets } = require('@yandex-int/archon-renderer-devserver-command');
const appendExpFlags = require('@yandex-int/frontend-kotik/middlewares/append-exp-flags');

module.exports = {
    routes: [
        {
            matcher: ...,
            handler: presets['serp-apphost-frontend-dynamic']
                // Добавление флагов делается после записи дампов, чтобы не менять исходные данные
                .addAfter('cache-writer', appendExpFlags());
            ...
        }
    ]
};
```

В коде теста:
```js
beforeEach(function() {
    return this.browser
        .yaOpenPage('/health/pills/product/shalfej-1211?&expFlags={"pills-new-article-card":1}&turnOffRandomArticles=true')
});
```

Query-параметр `expFlags` должен содержать json-encoded объект с флагами.

Можно указать этот query-параметр несколько раз, все указанные флаги будут добавлены в контекст. Уже добавленные в контекст флаги не убираются.

Плагин вызовет ошибку, если значение `expFlags` не может быть распаршено.

Плагин вызовет ошибку, если есть параметр `expFlags`, а в контексте нет айтемов с типом `experiments`.

Плагин вызовет ошибку, если требуется установить флаг, который уже установлен в контексте, даже если значение совпадает.

---

### Пресет для работы с json-форматом данных `frontend-json-preset`

Если у вас есть ajax-запросы и вам необходимо просто получить json-ответ от вашей ручки, этот пресет про это.
Пресет по сути похож на то, что раньше в `templar` делалось через параметр в конфиге `jsonPath`.

##### Как использовать

Создаем новый роут в массиве `routes` на нужный нам адрес для ajax-запросов и в хендлер добавляем пресет `frontend-json-preset`:

```js
'use strict';

const { presets } = require('@yandex-int/archon-renderer-devserver-command');
const JsonMiddlewares = require('./middlewares/json');


module.exports = {
    routes: [
        {
            matcher: ({ kotik: { parsedURL: { pathname } } }) => pathname.startsWith('/ugcpub'),
            handler: presets['serp-apphost-frontend-dynamic']
            // Если используем serp-apphost-frontend-dynamic, то добавляем json мидлвары после cacheReader мидлвара, поскольку именно после него
            // идут мидлвары про работу с апхостом и бинарными данными, что нам в случае с json данными не нужно.
                .addAfter('cacheReader', JsonMiddlewares.middlewares),
            context: {
                source: {
                    hostname: 'hamster.yandex.ru',
                    protocol: 'https'
                },
                // возможность добавить дополнительные заголовки запроса в источник
                headers: {
                    'x-yandex-https': 1
                },
                // список заголовков, которые должны пробрасываться от ответа источника в ответ kotik'a (по умолчанию не пробрасывается ничего)
                passHeaders: ['x-special-header'],
            }
        }
    ]
};
```

---

### Утилита для создания роутов-редиректов `utils/redirect.js`

Чтобы проще устанавливать простые редиректы в котике, частый пример использования, поставить редирект с корня `/` на путь вашего сервиса `/ugcpub/cabinet`

##### Как использовать

Импортируем утилиту и вызываем, указывая с какого пути в какой путь редиректить, утилита очень простая, больше никаких настроек нет.

```js
'use strict';

const getRedirectRoute = require('./middlewares/redirect');


module.exports = {
    routes: [
        getRedirectRoute({
            from: '/',
            to: '/ugcpub/cabinet'
        }),
        /*
        Код выше вернет обычный роут для котика:

            {
                matcher: ({ kotik: { parsedURL: { pathname } } }) => pathname === '/',
                handler: [
                    {
                        name: `redirect`,
                        fn(req, res) {
                            req.kotik.logger.debug(`Redirect request: from "/" to "/ugcpub/cabinet"`);

                            return res.redirect('/ugcpub/cabinet');
                        }
                    }
                ]
            }
         */

        /// Само собой утилиту можно вызывать много раз и создавать много различных редиректов.

        getRedirectRoute({
            from: '/ugcpub',
            to: '/ugcpub/cabinet'
        }),
        getRedirectRoute({
            from: '/ugcpub/public',
            to: '/ugcpub/pk'
        })
    ]
};
```
