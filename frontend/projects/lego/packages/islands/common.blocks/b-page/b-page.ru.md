# b-page

Используется для создания обвязки страницы. Отвечает за подключение CSS- и JS-файлов, выставление метатегов, заголовка, фавиконки и типа документа.

## Обзор

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [title](#field-title) (req) | `String` | Заголовок страницы. |
| [head](#field-head) | `BEMJSON` | Содержимое HTML-тега `<head>`. |
| [csp](#field-csp) | `Boolean`, `BEMJSON` | Добавление HTTP [Content-Security-Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP). |
| [charset](#field-charset) | `String` | Кодировка документа. По умолчанию: `utf-8`. |
| [doctype](#field-doctype) | `String` | Описание типа документа. По умолчанию: `<!DOCTYPE html>`. |
| [favicon](#field-favicon) | `String` | Фавиконка документа. |
| [meta](#field-meta) | `BEMJSON` | Метатеги документа. |
| [content](#field-content) | `String`, `BEMJSON` | Содержимое страницы. |

req — обязательное поле.

## Подробное описание

### Поля блока

<a name="field-title"></a>

#### Поле `title`

Определяет заголовок страницы. Выражается HTML-тегом `<title>`. **Обязательное**.

Тип: `String`.

```js
{
    block: 'b-page',
    title: 'Поле title',
    content: 'Поле title'
}
```

<a name="field-head"></a>

#### Поле `head`

Определяет содержимое HTML-тега `<head>`.

Тип: `BEMJSON`.

```js
{
    block: 'b-page',
    title: 'Поле head',
    head: [
        { elem: 'css', url: 'example1.css'},
        { elem: 'js', url: 'example1.js' }
    ],
    content: 'Поле head'
}
```

> **Примечание.** Также CSS-стили можно подключить с помощью элемента `link`.

<a name="field-csp"></a>

#### Поле `csp`

Определяет HTTP [Content-Security-Policy](http://www.w3.org/TR/CSP2/).

Выражается метатегом:

```html
<meta http-equiv="Content-Security-Policy" content="default-src ...">
```

Директивы HTTP Content-Security-Policy:

| Директивы | Значение | Назначение |
| --------- | -------- | ---------- |
| `default-src` | `self`, `https://yastatic.net` | Разрешенные источники, которые по умолчанию присваиваются незаданным директивам. [Директивы](http://www.w3.org/TR/CSP2/#directive-default-src) подпадающие под ограничения. |
| `script-src` | `self`, `https://yastatic.net` `yandex.ru`, `mc.yandex.ru`, `social.yandex.ru`, `export.yandex.ru`, `suggest.yandex.ru`, `notifications.yandex.ru` | Разрешенные источники для загрузки и выполнения JS. Политика запрещает выполнять инлайновые скрипты. Чтобы выполнить инлайновый скрипт, необходимо добавить к нему свойство `nonce`. |
| `style-src` | `self`, `https://yastatic.net`, `unsafe-inline` | Разрешенные источники для загрузки CSS. Политика разрешает выполнять инлайновые CSS-свойства. |
| `img-src` |`self`, `https://yastatic.net`, data: (`awaps.yandex.ru`, `kiks.yandex.ru`, `mc.yandex.ru`, `yabs.yandex.ru`,`avatars.yandex.net`, `www.tns-counter.ru`, `clck.yandex.ru`) | Разрешенные источники для загрузки изображений. Политика разрешает использовать  инлайновые картинки закодированные методом `base64`. |
| `connect-src` | `self`, `mc.yandex.ru` | Политика ограничивает источники, к которым можно подключаться с помощью: XMLHttpRequest, WebSocket, EventSource, sendBeacon(url). При использовании WebSocket, необходимо указывать полный `uri` (wss://websocket-host.yandex.ru), потому что по умолчанию протокол страницы — `https:`. |

> **Примечание.** Чтобы переопределить политику безопасности, проконсультируйтесь с СБ.

Тип: `Boolean`, `BEMJSON`.

```js
{
    block: 'b-page',
    title: 'Поле csp',
    csp: {
        elem: 'csp',
        nonce: '2726c7f26c1'
    },
    content: 'Поле csp'
}
```

<a name="field-charset"></a>

#### Поле `charset`

Определяет кодировку документа. По умолчанию: `utf-8`.

Тип: `String`.

```js
{
    block: 'b-page',
    title: 'Поле charset',
    charset: 'utf-16',
    content: 'Поле charset'
}
```

<a name="field-doctype"></a>

#### Поле `doctype`

Определяет тип документа. По умолчанию: `<!DOCTYPE html>`.

Тип: `String`.

```js
{
    block: 'b-page',
    title: 'Поле doctype',
    doctype: '<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">',
    content: 'Поле doctype'
}
```

<a name="field-favicon"></a>

#### Поле `favicon`

Определяет фавиконку документа.

Тип: `String`.

```js
{
    block: 'b-page',
    title: 'Поле favicon',
    favicon: 'favicon.ico',
    content: 'Поле favicon'
}
```

<a name="field-meta"></a>

#### Поле `meta`

Определяет метатеги документа.

Тип: `String`.

```js
{
    block: 'b-page',
    title: 'Поле meta',
    meta: [
        {
            elem: 'meta',
            attrs: {
                name: 'keywords',
                content: 'islands, componets'
            }
        },
        {
            elem: 'meta',
            attrs: {
                name: 'description',
                content: 'Yet another library'
            }
        }
    ],
    content: 'Поле meta'
}
```

<a name="field-content"></a>

#### Поле `content`

Определяет содержимое документа.

Тип: `String`, `BEMJSON`.

```js
{
    block: 'b-page',
    title: 'Поле content',
    content: {
        block: 'link',
        mods: { theme: 'pseudo', pseudo: 'yes' },
        url: '#',
        target: '_blank',
        title: 'Кликни меня',
        text: 'Поле content'
    }
}
```