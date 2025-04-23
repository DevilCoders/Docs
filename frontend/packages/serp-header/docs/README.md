# Подсказки для разработчиков ванильных компонентов

### Кейсы
1. [Вставка значений в шаблон](#insert)
1. [Обработка объектов в параметрах](#handle)
1. [Рендер по условию](#render)
1. [Создание нового блока](#new)

<a name="insert"></a>
### Вставка значений в шаблон

Можно использовать две строковые конструкции:
- `'_{{имяКлюча}}_'` — позволяет получить значение по указанному ключи из текущего `ctx`. В качестве имени ключа берётся всё, что написано внутри конструкции, вложенность не поддерживаются.
- `'_{{(JS-код)}}_'` — позволяет написать произвольный JS-код, который будет выполнен, и результат передан в шаблон. Можно использовать `ctx.*` для доступа к значениях контекста, при этом возможен доступ ко вложенным свойствам.

В обоих случаях, при вставке в шаблон значение приводится к строке. Следовательно, в коде `'_{{myObject}}_'` в шаблон вставится `'[object Object]'`, для `typeof '_{{(ctx.myObject)}}_'` будет `'string'`, но для `'_{{(typeof ctx.myObject)}}_'` будет `'object'`.

<a name="handle"></a>
### Обработка объектов в параметрах

Так как все значения при вставки в `*.bemhtml.js` приводятся к строке, код, работающий с ними, нужно писать прямо в строках внутри `'_{{(…)}}_'`.

Например, для вывода списка:

```js
block('my-block')(
    content()(function() {
        const itemHtml = this.reapply({
            block: this.block,
            elem: 'item',
            ...apply('item-params'),
        });

        return `_{{(ctx.items ? ctx.items.map(ctx => \`${
            itemHtml
        }\`).join('') : '')}}_`;
    }),
    mode('item-params')({
        // В элементе my-block__item можно использовать эти значения из ctx
        text: '_{{text}}_',
        // Можно прокинуть и объекты, работая с ними внутри `_{{(ctx.items.map(…))}}_`
        items: '_{{items}}_',
    })
);
```

<a name="render"></a>
### Рендер по условию

Если в шаблон нужно вставить разные блоки (или одинаковый, но с разным набором параметров) в зависимости от параметра, нужно подготовить HTML для каждого варианта заранее и «разрулить» их на уровне кода в строке-подстановке:

```js
    content()(function() {
        const linkHtml = this.reapply({
            block: this.block,
            elem: 'link',
            tag: 'a',
            attrs: {
                href: '_{{(ctx.url)}}_',
            },
            content: this.ctx.text,
        });
        const buttonHtml = this.reapply({
            block: this.block,
            elem: 'link',
            tag: 'button',
            attrs: {
                type: 'button',
            },
            content: this.ctx.text,
        });

        return `_{{(ctx.url ? \`${linkHtml}\` : \`${buttonHtml}\`)}}_`;
    })
```

Если различаются только значения параметров, то хватит и тернарников внутри `'_{{(…)}}_'`.

<a name="new"></a>
## Создание нового блока

### Клиентский JS

Нужно создать класс и инициализировать его на элементах блока.

```js
(/** @param {*} window */function(window) {
    'use strict';

    /**
     * CSS-имя блока
     */
    const BLOCK = 'my-block';

    /**
     * Блок MyBlock
     */
    class MyBlock {
        /**
         * @param {HTMLElement} element DOM-элемент блока
         */
        constructor(element) {
            this._element = element;
        }
    }

    window.Lego = window.Lego || {};
    window.Lego.MyBlock = MyBlock;

    for (const blockNode of document.querySelectorAll('.' + BLOCK)) {
        // eslint-disable-next-line no-new
        new MyBlock(/** @type {HTMLElement} */(blockNode));
    }
})(window);
```

### Превью

В файл `packages/serp-header/data/tools-header.data.js` нужно добавить вставку компонента примерно таким кодом:
```js
myBlockHTML: myBlock.getContent({ ctx: {} }) + '<script>' + myBlock.getContent({ content: 'js' }) + '</script>',
```

Также, рядом нужно создать файл для самого блока:
```js
const base = {
    key: 'base',
    block: 'my-block',
};

module.exports = {
    platforms: ['desktop', 'touch-phone'],
    services: {
        base: [
            base,
        ],
    },
    generateTest: false,
    neededJsBlocks: [
    ],
    examples: [
        {
            ctx: {},
        },
    ],
};
```

Добавляем элемент в шапку, создав файл `packages/serp-header/common.blocks/tools-header/__my-block/tools-header__my-block.bemhtml.js`:
```js
block('tools-header').elem('my-block')(
    content()(function() {
        return '_{{(ctx.myBlockHTML || "")}}_';
    }),
);
```

В файле `packages/serp-header/common.blocks/tools-header/tools-header.bemhtml.js` нужно вставить блок в шапку. Чтобы наличие блока в шапке было опциональным, можно использовать `mode('insert-when')`:
```js
    mode('insert-when')(function() {
        const { when, block, elem } = this;
        const html = applyCtx({ block, elem });

        return `_{{(ctx.${when} && \`${html}\` )}}_`;
    })
```

Тогда вставка будет выглядеть так:
```js
apply('insert-when', { elem: 'my-block', when: 'myBlockHTML' }),
```