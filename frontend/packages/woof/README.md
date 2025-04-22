# Wiki Formatter

## Установка

```sh
npm i -S @yandex-int/woof --registry https://npm.yandex-team.ru
```

### Внешние зависимости

- [jQuery](https://jquery.com/) 2.2+ [[cdn](https://yastatic.net/jquery/2.2.3/jquery.min.js)]
- [Socket.IO](https://socket.io) [[cdn](https://yastatic.net/s3/frontend/woof/_/socket.io.2.2.0.js)]

## Подключение

### Действия на сервере

Начать нужно с того, что на сервере использовать пакет `@yandex-int/woof`:

```js
const { create } = require('@yandex-int/woof');
```

Функция `create()` создаст серверный инстанс форматтера, который позволяет сделать следующее:

1. Рендерить разметку на сервере
1. Получить код клиентского, скомпилированного форматтера
1. Сконфигурировать как клиентский, так и серверный инстанс форматтера

Созданный инстанс получит [дефолтные настройки](src/settings.js),
которые можно переопределить, передав в `create()` объект который будет глубоко смержен с настройками по-умолчанию:

```js
const formatter = create({
    lang: 'en',
    instance: 'business',
});
```

Список возможных настроек можно посмотреть [здесь](server.d.ts#L39)

Когда инстанс готов, можно рендерить вики разметку:

```js
const ast = require('@yandex-int/remark-woofmd').parseWikiMd('**Bold**', formatter.getConfig());
const bemjson = await require('@yandex-int/woofmd-to-bemjson').formatMdAst(ast, formatter.getConfig());
const html = await formatter.bemjsonToHtml(bemjson);
```

**ВАЖНО:** Чтобы рендерить разметку на сервере, нужно заказать сетевую дырку от сети,
в которой работает сервер, до [schi_url](src/server.d.ts#L82) (по умолчанию это `https://schi.yandex-team.ru`),
иначе корректная работа форматтера не будет возможной

Это готовая для рендеринга html разметка, которую нужно доставить в браузер через шаблоны.

Вместе с разметкой на клиент нужно доставить стили и код клиентской части форматтера.
Чтобы получить код браузерной части форматтера, необходимо вызывать функцию `getBrowserCode()` серверного инстанса:

```js
const {
    stylesheetRemoteChunks,
    javascriptInlineChunks,
    javascriptRemoteChunks,
} = formatter.getBrowserCode();
```

Константы `stylesheetRemoteChunks` и `javascriptRemoteChunks` являются списками URL (String), указывающими на CDN,
и их нужно подключить вместе с другими ресурсами html страницы.

Константа `javascriptInlineChunks` является списком строк кода, которые нужно проинициализировать ДО подключения `javascriptRemoteChunks`:

```js
BEMHTML.apply([
    ...javascriptInlineChunks.map((src) => ({
        tag: 'link',
        attrs: {
            rel: 'stylesheet',
            href: src,
        },
    })),
    ...javascriptInlineChunks.map((src) => ({
        tag: 'script',
        attrs: { nonce },
        content: { html: src },
    })),
    ...javascriptRemoteChunks.map((src) => ({
        tag: 'script',
        attrs: { src },
    })),
])
```

В `javascriptInlineChunks` содержится код, который доопределит базовые настройки браузерного
форматтера переданными дополнительными настройками на сервере.
То есть, если вы на сервере при вызове `create()` передавали туда любые кастомные настройки,
то и на клиент они тоже приедут через `javascriptInlineChunks`.

### Действия в браузере

Теперь, имея в браузере отрендеренную разметку и подключенные ресурсы,
нужно проинициализировать форматтер:

```js
const formatter = new Ya.FormatterViewPort({
    // Нужно передать ссылку на элемент, внутри которого находится wiki-разметка
    domElem: document.querySelectorAll('.wf-viewport'),
    settings: {
        // Любые дополнительные настройки
    },
});
```

С этого момента все готово, стили отображаются, DOM форматтера живой.

## Рецепты

### Динамический рендер

Чтобы рендерить разметку динамически (по нажатию на кнопку, etc.), есть метод `.render()` у проинициализированного браузерного форматтера:

```js
formatter.render('*Italic*');
```

### Рендер на клиенте в строку

Чтобы отрендерить разметку в строку, чтобы после этого ее использовать как угодно,
нужно воспользоваться методом браузерного инстанса:

```js
const html = await formatter.renderToString('*Italic*');
```

После этого можно встроить ее куда угодно, например использовать в шаблонах:

```js
BEMHTML.apply({
    block: 'wf-viewport',
    content: { html },
});
```

После того, как html попадет в DOM, нужно будет просто проинстанцировать форматтер на необходимом узле:

```js
new Ya.FormatterViewPort({ domElem: document.querySelector('.wf-viewport') });
```

### Удаление DOM форматтера

Чтобы удалить DOM форматтера, нужно вызывать `.remove()`:

```js
formatter.remove();
```

## API

### Серверный инстанс

#### create(settings?: [IWoofSettings](server.d.ts#L39)): [IServerInstance](server.d.ts#L3)

Создает серверный инстанс для SSR и получения кода браузерного бандла:

```js
const { create } = require('@yandex-int/woof');

const formatter = create();
```

*Описание методов и настроек серверного инстанса можно найти [здесь](server.d.ts)*

### Браузерный инстанс

#### new Ya.FormatterViewPort(params: [IFormatterViewportParams](src/client.d.ts#L3))

Создает браузерный инстанс:

```js
const formatter = new Ya.FormatterViewPort({
    domElem: document.querySelector('.wf-viewport'),
});
```

*Описание методов и настроек браузерного инстанса можно найти [здесь](src/client.d.ts)*

---

*Все, что не описано в документации, вы используете на свой страх и риск*.

По всем вопросам можно писать разработчикам интерфейсов команды [Вики](https://abc.yandex-team.ru/services/_wiki_/?scope=development)
