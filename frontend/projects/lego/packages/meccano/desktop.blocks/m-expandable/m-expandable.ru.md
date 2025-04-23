## m-expandable
Примешивается к другому блоку, для добавления эффекта схлопывания.

### HowTo
* Подмешать к вашему блоку `m-expandable`;
* Подмешать к переключателю `m-expandable elem trigger`;
* Подмешать к схлопывающейся части `m-expandable elem cropper`, или просто вставить контент этот элемент.


### Базовый вариант, без анимации

```bemjson
{
    block: 'island',
    mix: { block: 'm-expandable', js: true },
    content: [
        {
            block: 'link', mods: { pseudo: 'yes' },
            mix: { block: 'm-expandable', elem: 'trigger' }, // Активатор переключения
            content: 'Переключатель'
        },
        {
            block: 'm-expandable',
            elem: 'cropper', // Элемент, который будет схлопываться
            content: ['Что-то там']
        }
    ]
}
```

### Базовый вариант, с анимацией

```bemjson
{
    block: 'island',
    mix: {
        block: 'm-expandable',
        js: true,
        mods: { animated: 'yes' }
    },
    content: [
        {
            block: 'link', mods: { pseudo: 'yes' },
            mix: { block: 'm-expandable', elem: 'trigger' }, // Активатор переключения
            content: 'Переключатель'
        },
        {
            block: 'm-expandable',
            elem: 'cropper', // Элемент, который будет схлопываться
            content: ['Что-то там']
        }
    ]
}
```

### Схлопнутый вариант, без анимации

```bemjson
{
    block: 'island',
    mix: {
        block: 'm-expandable',
        js: true,
        mods: { collapsed: 'yes' }
    },
    content: [
        {
            block: 'link', mods: { pseudo: 'yes' },
            mix: { block: 'm-expandable', elem: 'trigger' }, // Активатор переключения
            content: 'Переключатель'
        },
        {
            block: 'm-expandable',
            elem: 'cropper', // Элемент, который будет схлопываться
            content: ['Что-то там']
        }
    ]
}
```

### Схлопнутый вариант, с анимацией

```bemjson
{
    block: 'island',
    mix: {
        block: 'm-expandable',
        js: true,
        mods: { animated: 'yes', collapsed: 'yes' }
    },
    content: [
        {
            block: 'link', mods: { pseudo: 'yes' },
            mix: { block: 'm-expandable', elem: 'trigger' }, // Активатор переключения
            content: 'Переключатель'
        },
        {
            block: 'm-expandable',
            elem: 'cropper', // Элемент, который будет схлопываться
            content: ['Что-то там']
        }
    ]
}
```

### Вариант с `_autocrop_yes`
Модификатор `_autocrop` позволяет выставлять `_collapsed_yes` автоматически.

Для этого нужно стилями задать свернутому `__cropper` ненулевую высоту.

```css
.example_autocrop .m-expandable__cropper_collapsed_yes
{
    height: 30px !important; /* important обязательно */
}
```

И выставить блоку `m-expandable` модификатор `_autocrop_yes`.

```bemjson
{
    block: 'example_autocrop',
    mix: {
        block: 'm-expandable',
        js: true,
        mods: {
            autocrop: 'yes',
            collapsed: 'yes'
        }
    },
    content: [
        {
            block: 'm-expandable',
            elem: 'cropper',
            elemMods: {collapsed: 'yes'},
            content: 'Контент'
        },
        {
            block: 'm-expandable',
            elem: 'trigger',
            content: 'Переключатель'
        }
    ]
}
```

Теперь если высота содержимого `__cropper` будет больше чем заданная в CSS, то:
* Блок `m-expandable` получит модификатор `_cropped_yes`;
* Блок останется в свернутом состоянии;
* `__trigger` будет виден.

В противном случае:
* Блок `m-expandable` получит модификатор `_cropped_no`;
* Блок развернётся (потеряет модификатор `_collapsed_yes`);
* `__trigger` будет скрыт.

Пересчитать высоту содержимого `__cropper` можно методом `checkContent`.

### Events
#### collapsed
Срабатывает перед установкой модификатора `collapsed`.

#### expanded
Срабатывает перед удалением модификатора `collapsed`.

### API
#### .toggle(mode)
```javascript
@param {Boolean} mode — свернуть или развернуть
```
Свернуть или развернуть.

#### .expand()
Развернуть.

#### .collapse()
Свернуть.
