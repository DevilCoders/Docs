## Описание
Блок `b-page` создает базовую обвязку страницы – теги верхнего уровня: `<html>`, `<head>`, `<body>`.
Отвечает за подключение необходимых CSS и JS файлов к странице, выставление типа текущего документа, метатегов, заголовка, фавиконки и прочих данных.

В «островном» блоке `b-page`, доопределяются атрибут `lang` тега `<html>`.

Глобальный атрибут `lang` тега `<html>` (для указания языка документа) добавляется в BEMHTML-шаблоне блока, на текущем уровне переопределения. Значение атрибута определяется из параметра `lang` блока [i-global](../i-global/i-global.ru.md). По умолчанию выставляется – `ru` (русский язык).

В блоках, зависящих от глобальных параметров, разработчику необходимо самостоятельно описать mustDeps-зависимость от блока `i-global`:

```js
({
    mustDeps: [
        { block: 'i-global' }
    ]
});
```

### Объявление блока на странице

Декларация блока в BEMJSON начинается объявлением блока и указанием свойства `title`, которое превращается в тег `<title>` в HTML.

```js
{
    block: 'b-page',
    title: 'Page with link',
    content: 'Page'
}
```

Указание свойства `head` дополняет элемент `head`, соответствующий HTML-тегу `<head>`, элементами для подключения CSS и JS файлов:

```js
{
    block: 'b-page',
    title: 'Page with link',
    head: [
        { elem: 'css', url: 'example.css'},
        { elem: 'js', url: 'example.js' }
    ],
    content: 'Page'
}
```

Элемент `css` превращается в HTML-тег `<link>`, подключающий как CSS-стиль тот файл, что указан в свойстве `url` этого элемента.

Также есть возможность указывать свойство `content` для содержания тега `<style>`:

```js
{
    block: 'b-page',
    title: 'Page with link',
    head: [
        {
            elem: 'css',
            content: '.b-blah { color: #f00 }'
        }
    ],
    content: 'Page'
}
```

Каждому элементу `css` можно добавить свойство `ie`, которое позволит использовать условные комментарии (`condittional comments`).
Если это свойство `false`, то будут использоваться условные комментарии, которые предотвратят использование этих стилей в IE. При строчном значении этого свойства тег `<link>`, будет обернут в соответствующий `conditional comment`, и этот стиль будет загружаться и использоваться только в указанных браузерах.

Условные комментарии для изменения стиля для браузера IE8+

```bemjson
{
    block: 'b-page',
    title: 'Page with link',
    head: [
        { elem: 'css', url: 'example.css', ie: false },
        { elem: 'css', url: 'example.ie8.css', ie: 'gte IE 8' },
        { elem: 'js', url: 'example.js' }
    ],
    content: 'Page'
}
```

Элемент `js` действует аналогично, подключая к странице JS-файлы при помощи тега `<script>`.

Свойство `head` не описывает содержание HTML-тега `<head>` полностью, а лишь дополняет заданное по умолчанию, которое блок сам создаёт в своём BEMHTML-шаблоне.

#### Тег `<meta>` с указанием кодировки

```javascript
content: [
...
{
    tag: 'meta',
    attrs: { 'http-equiv': 'content-type', content: 'text/html; charset=utf-8' }
},
...
```

Тег `<meta>` для использования IE9+ в максимальном **compatibility** режиме, BEMHTML:

```javascript
content: [
...
{
    tag: 'meta',
    attrs: { 'http-equiv': 'X-UA-Compatible', content: 'IE=EmulateIE7, IE=edge' }
},
...
```



#### Выставление значения тега `<title>` страницы из свойства

```javascript
content: [
...
{
    tag: 'title',
    content: this.ctx.title
},
...
```


#### Выставление фавиконки

```javascript
content: [
...
this.ctx.favicon ? {
    elem: 'favicon',
    url: this.ctx.favicon
} : '',
...
```


#### Декларация блока `i-ua`

```javascript
content: [
...
{
    block: 'i-ua'
},
...
```

Аналогично указанию свойства `head`, может быть задано свойство `meta`, содержащее один или несколько элементов `meta`:

```bemjson
{
    block: 'b-page',
    title: 'Page with link',
    meta: {
        elem: 'meta',
        attrs: {
            name: 'keywords',
            content: 'js, css, html'
        }
    },
    content: 'Page'
}
```

```bemjson
{
    block: 'b-page',
    title: 'Page with link',
    meta: [
        {
            elem: 'meta',
            attrs: {
                name: 'keywords',
                content: 'js, css, html'
            }
        },
        {
            elem: 'meta',
            attrs: {
                name : 'description',
                content : 'Yet another webdev blog'
            }
        }
    ],
    content: 'Page'
}
```

Значением свойства `content` блока `b-page` может быть хеш-описание содержимого (если речь идёт лишь об одном блоке) или массив блоков, описанных хешами:

```bemjson
{
    block: 'b-page',
    title: 'Page with link',
    content: {
        block: 'link',
        mods: { theme: 'pseudo', pseudo: 'yes' },
        url: '#',
        target: '_blank',
        title: 'Кликни меня',
        text: 'Псевдоссылка, меняющая цвет по клику'
    }
}
```

На блоки, содержащиеся в `content`, действуют их BEMHTML-шаблоны.

#### Масштабирование страницы

Для мобильных устройств (touch-уровень) блок `b-page` позволяет задать содержимое метатегу `viewport` с помощью поля `zoom`. 

Если во входном BEMJSON блока задано поля `zoom` в значении `true` — масштабирование включено (`<mata name="viewport" content="width=device-width,initial-scale=1">`), если поле отсутствует – масштабирование отключено (`<mata name="viewport" content="width=device-width,maximum-scale=1,initial-scale=1,user-scalable=0">`).


```bemjson
{
    block: 'b-page',
    title: 'Page with zoom',
    zoom: true,
    content: 'MyPage'
}
```


#### Отмена автоматической инициализации блоков

```javascript
noDeps: [
    { block: 'i-bem', elem: 'dom', mods: { init: 'auto' } }
]
```
## Content-Security-Policy

Блок `b-page` позволяет подключить метатег `<meta http-equiv="Content-Security-Policy" content="[POLICY GOES HERE]">`, который устанавливает [политику безопасности по умолчанию](#default-csp-policy), для загрузки контента (скриптов, стилей, картинок и т. д.).

---
**NB** Обратите внимание, что по умолчанию метатег отключен.

---

Подробнее о `Content Security Policy`:

* http://www.w3.org/TR/CSP2/
* https://wiki.yandex-team.ru/product-security/csp/
* https://wiki.yandex-team.ru/lego/csp/
* https://github.yandex-team.ru/lego/islands-guidelines/blob/master/content-security-policy.md


<a name="default-csp-policy"></a>
### Политика по умолчанию

|Директивы      | Значение      | Назначение  |
| ------------- |---------------| ----------  |
| default-src   | `'self'`<br>`https://yastatic.net` | Разрешенные источники, которые по умолчанию присваиваются не заданным директивам. [Директивы](http://www.w3.org/TR/CSP2/#directive-default-src) подпадающие под ограничения, заданные в `default-src`.<br> _**Внимание**: Специализированные директивы для соответствующего ресурса, `script-src`, не наследуют, а полностью переопределяют директиву default-src`._|
|script-src| 'self'<br>https://yastatic.net<br>yandex.ru<br>mc.yandex.ru<br>social.yandex.ru<br>export.yandex.ru<br>suggest.yandex.ru<br>notifications.yandex.ru |Разрешенные источники для загрузки и выполнения JS-скриптов.<br> _**Внимание**: Политика запрещает выполнять инлайновые скрипты (не указано 'unsafe-inline'). При необходимости в inlain-скриптах, нужно добавить к скрипту свойство `nonce`._ |
|style-src|'self'<br>https://yastatic.net<br>unsafe-inline|Разрешенные источники для загрузки CSS-стилей.<br>_**Внимание**: политика разрешает выполнять inline-стили (указано 'unsafe-inline'). <br>Например, блоку [popup](../popup/popup.ru.md) нужно динамически задавать размер через изменение инлайн CSS: <code>this.domElem.css(dimensions);</code>_.|
|img-src|'self'<br>https://yastatic.net<br>data:<br>awaps.yandex.ru<br>kiks.yandex.ru<br>mc.yandex.ru<br>yabs.yandex.ru<br>avatars.yandex.net<br>www.tns-counter.ru<br>clck.yandex.ru|Разрешенные источники для загрузки изображений.<br>_**Внимание**: политика разрешает использовать inline-картинки base64 (указан протокол «data:»)._ |
|frame-src| 'self'<br>https://yastatic.net<br>awaps.yandex.ru<br>pass.yandex.ru<br>legal.yandex.ru<br>notifications.yandex.ru| Разрешенные источники для загрузки фреймов. [Директива устарела](http://www.w3.org/TR/CSP2/#directive-frame-src) в пользу `child-src`, но пока в браузерах поддерживается только `frame-src`.|
|connect-src|'self'<br>mc.yandex.ru| Ограничивает источники, к которым можно подключаться с помощью:<ul><li>XMLHttpRequest</li><li>WebSocket</li><li>EventSource</li><li>атрибут ping в элементе &lt;a&gt;</li><li>sendBeacon(url)</li></ul>_**Внимание**: При использовании WebSocket надо писать полный `uri` wss://websocket-host.yandex.ru, так как по умолчанию протокол страницы `https:`_|

**NB** Обратите внимание,если в заголовке CSP указать хост без схемы, например `social.yandex.ru`, то он отработает для того протокола, по которому пришел пользователь. То есть при заходе по `http://yandex.ru`, адрес `https://social.yandex.ru` будет заблокирован CSP. [Подробнее](https://st.yandex-team.ru/PORTALADMIN-212#1427902306000). [Особенности сопоставления URI политики](http://www.w3.org/TR/CSP/#source-list-path-patching).

На сервисе политику по умолчанию можно [подключить](#add-csp) несколькими способами или [переопределить](#redef-csp).


<a name="add-csp"></a>
### Подключение политики по умолчанию

Политика безопасности подключается несколькими способами, которые различаются областью применения: в пределах страницы или всего сервиса.

#### Локальное подключение

Подключить политику только для отдельной страницы сервиса можно в поле `csp` BEMJSON блока. Рекомендуемый способ.

```javascript
{
    block: 'b-page',
    csp: true
}
```

Метатег с CSP будет расположен сразу после тега `<html>`. Политика применяется ко всем
ресурсам страницы расположенным в `<head>` (как внешних, подключенных по ссылке `<link>`, так и добавляемых в самом документе).


Есть дополнительная возможность подключить политику в элементе блока `csp` в поле `head`. В этом случае, метатег будет последним элементом в `<head>`.

---
**NB** Этот способ применять не рекомендуется, так как код загружаемый до метатега CSP не проверяется на соответствие политике безопасности. Например, данные плагинов для браузеров.

---

```javascript
{
    block: 'b-page',
    head: [
        { elem: 'csp': csp: true }
    ]
}
```

#### Глобальное подключение

Подключить политику для всего сервиса можно переопределив шаблон BEMHTML/BH элемента блока `csp`.

**BEMHTML**

```javascript
block('b-page').elem('csp').def()(function(){
    this.ctx.policies = true;
    applyNext();
});
```

**BH**

```javascript
module.exports = function(bh) {
    bh.match('b-page__csp', function(ctx) {
        ctx.param('policies', true);
    });
};
```

_При использовании опционального элемента `csp`, подключите его в зависимости блока._

<a name="redef-csp"></a>

### Переопределение политики

---
**NB** Если вы планируете переопределять политику по умолчанию, проконсультируйтесь со <a href="mail:product-security@yandex-team.ru">службой безопасности</a>.

---

Способы переопределения политики аналогичны перечисленным в разделе [Подключение политики](#add-csp). Но предварительно нужно указать разрешенные источники в списке требуемых директив.

Переопределять можно как [директивы](#default-csp-policy) заданные в политике по умолчанию, так и любые из списка [директив](http://www.w3.org/TR/CSP2/#directive
), реализованные в CSP2.

Следует помнить, что директивы `report-uri` и `sandbox` нельзя задать через метатег (согласно спецификации, в метатеге они игнорируются).

**NB** Обратите внимание, что при переопределении директив из политики по умолчанию они не расширяются, а заменяются новым значением. Чтобы добавить новый ресурс директиве, необходимо также указать значения, которые были в политике по умолчанию.

Новое значение заменяет значение по умолчанию директивы `style-src`:

```javascript
({
    block: 'b-page',
    csp: {
        policies: {style-src: ['new-url']}
    }
})
```

Добавление нового значения:

```javascript
({
    block: 'b-page',
    csp: {
        policies: {style-src: ["'self'", 'https://yastatic.net', "'unsafe-inline'", 'new-url']}
    }
})
```

#### Локальное переопределение

В поле `csp` BEMJSON блока. Значение каждой директивы – массив разрешенных источников. Рекомендуемый способ.

```javacsript
({
    block: 'b-page',
    csp: {
        policies: {
            'script-src': [
                'from-bemjson.net',
                'example.com'
            ],
            style-src': [
                'mystyle.net'
            ]
        }
    }
});
```

Список источников в каждой директиве можно [гибко настроить](https://lego.yandex-team.ru/guidelines/security-policy/#Источники).

```javacsript
({
    block: 'b-page',
    csp: {
        policies: {
            'script-src': [
                'from-bemjson.net',
                'example.com'
            ],
            style-src': [
                'self',
                'data: example.com'
            ]
        }
    }
});
```

Переопределение политики в элементе блока `csp` в поле  блока `head`. Не рекомендуется использовать (способ небезопасный).

 ```javascript
 ({
    block: 'b-page',
    head: [
        {
            elem: 'csp',
            policies: {
                'script-src': [
                    'from-bemjson.net',
                    'example.com'
                ],
                'style-src': [
                    'mystyle.net'
                ]
            }
        }
    ]
});
 ```

#### Глобальное переопределение

Выполняется переопределением шаблонов элемента блока `csp`.

**BEMHTML**

```javascript
block('b-page').elem('csp').def()(function(){
    this.ctx.policies = {'script-src': ['test-from-bemhtml.net']};
    applyNext();
});
```

**BH**

```javascript
module.exports = function(bh) {
    bh.match('b-page__csp', function(ctx) {
        ctx.param('policies', {'script-src': ['test-from-bemhtml.net']});
    });
};
```

<a name="nonce"></a>
### Передача nonce

Для директив `script-src` и `style-src` существует специальное значение `nonce`, которое позволяет задать уникальный ключ `$RANDOM`.

`nonce-$RANDOM` разрешает использовать инлайновый JavaScript (`<script>`) и инлайновый CSS (`<style>`), у которых атрибут `nonce` равен `$RANDOM`. Их содержимое не будет заблокировано даже при отсутствии ключевого слова `unsafe-inline`.

Значение по умолчанию для `nonce` берется из блока `i-global`(рекомендуемый способ):

```javascript
// BEMHTML
this['i-global'].nonce

// BH
bh.lib.global.nonce
```

Передать свое значение `nonce` можно в поле элемента `csp` BEMJSON блока:

```javascript
// TODO: https://st.yandex-team.ru/ISLROMOCHKA-229
({
    block: 'b-page',
    csp: {
        nonce: 'EDNnf03nceIOfn39fn3e9h3sdfa'
    }
});
```

В этом случае, к директивам `script-src` и `style-src` будет добавлено значение `'nonce-EDNnf03nceIOfn39fn3e9h3sdfa'`. Этим значением подписываются (добавляется свойство nonce="%nonce%") в блоки:

* i-ua: `<script nonce="%переданное значение nonce%">тут код блока i-ua</script>`
* i-jquery, будет подключен как `<script src="_50-js-css-nonce.js"></script>`
и элементы `css`  и `js` блока `b-page`.

Это позволит добавлять на страницу инлайн-скрипты и стили с атрибутом `nonce-EDNnf03nceIOfn39fn3e9h3sdfa`.

Стили и скрипты, разрешенные с помощью `nonce`:

```html
<script nonce="EDNnf03nceIOfn39fn3e9h3sdfa">
    alert("Allowed because nonce is valid.");
</script>
<style nonce="EDNnf03nceIOfn39fn3e9h3sdfa">
    .inline {}
</style>
```
