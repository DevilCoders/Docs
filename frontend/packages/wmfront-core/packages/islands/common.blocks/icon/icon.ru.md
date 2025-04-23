# icon

Используется для создания иконок.

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [type](#mods-type) | `'arrow'`, `'filter'`, `'close'`, `'cross'`, `'cross-websearch'` | `BEMJSON` | Тип иконки. |
| [size](#mods-size) | `'xs'`, `'s'` | `BEMJSON`, `JS` | Размер иконки. |
| [direction](#mods-direction) | `'left'`, `'top'`, `'right'`, `'bottom'` | `BEMJSON` | Направление иконки-стрелки (`_type_arrow` и `_glyph_type-arrow`). |
| [action](#mods-action) | `'filter'`, `'settings'`, `'tableau'` | `BEMJSON`, `JS` | Иконки-действия. |
| [glyph](#mods-glyph) | `'carets-v'`, `'type-arrow'`, `'type-check'`, `'type-close'`, `'type-cross'`, `'type-filter'`, `'type-tick'`, `'x-sign'` | `BEMJSON`, `JS` | Инлайновые SVG-иконки. |

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [url](#field-url) | `String` | Адрес иконки. |

## Подробное описание

### Модификаторы блока

<a name="mods-type"></a>

#### Модификатор `type`

Задает тип иконки.

Допустимые значения: `'arrow'`, `'filter'`, `'close'`, `'cross'`, `'cross-websearch'`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['arrow', 'filter', 'close', 'cross', 'cross-websearch'],
    body: [
        ['arrow', 'filter', 'close', 'cross', 'cross-websearch'].map(function(type) {
            return {
                block: 'x-area',
                mods: { bordered: 'yes' },
                content: {
                    block: 'icon',
                    attrs: { style: 'width: 16px; height: 16px;' },
                    mods: { type: type }
                }
            };
        })
    ]
}
```

<a name="mods-size"></a>

#### Модификатор `size`

Задает размер иконке.

Допустимые значения: `'xs'`, `'s'`, `'m'`.

Способ установки: `BEMJSON`, `JS`.

> **Важно!** Модификатор `size` используется не со всеми иконками. В большинстве случаев его определять необязательно.

```js
{
    block: 'x-area',
    content: {
        block: 'x-table',
        xhead: [''].concat(['xs', 's', 'm', '—']),
        yhead: [''].concat(['_type_arrow', '_glyph_type-arrow', '_glyph_type-cross', '_glyph_x-sign']),
        body: [
                { name: 'type', st: 'opt', mods: { type: 'arrow' } },
                { name: 'glyph', st: 'opt', mods: { glyph: 'type-arrow' } },
                { name: 'glyph', st: 'opt', mods: { glyph: 'type-cross' } },
                { name: 'glyph', st: 'req', mods: { glyph: 'x-sign' } }
            ].map(function(obj) {
            return ['xs', 's', 'm', undefined].map(function(size) {
                switch (size) {
                  case 's':
                    return obj.st === 'opt' ? { block: 'x-area',
                    content: '—' } : {
                        block: 'x-area',
                        mods: { bordered: 'yes' },
                        content: [
                            {
                                block: 'icon',
                                mods: Object.assign({}, obj.mods, { size: size })
                            },
                            {
                                elem: 'caption',
                                content: obj.st
                            }
                        ]
                    };
                    break;
                  case 'm':
                    return obj.st === 'opt' ? { block: 'x-area',
                    content: '—' } : {
                      block: 'x-area',
                      mods: { bordered: 'yes' },
                      content: [
                          {
                              block: 'icon',
                              mods: Object.assign({}, obj.mods, { size: size })
                          },
                          {
                              elem: 'caption',
                              content: obj.st
                          }
                      ]
                    };
                    break;
                  case undefined:
                    return obj.st === 'req' ? { block: 'x-area',
                    content: '—' } : {
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    content: [
                        {
                            block: 'icon',
                            attrs: obj.name === 'type' ? { style: 'width: 16px; height: 16px;' } : undefined,
                            mods: Object.assign({}, obj.mods, { size: size })
                        },
                        {
                            elem: 'caption',
                            content: obj.st
                        }
                    ]
                    };
                    break;
                  default:
                    return {
                        block: 'x-area',
                        mods: { bordered: 'yes' },
                        content: [
                            {
                                block: 'icon',
                                attrs: obj.name === 'type' ? { style: 'width: 16px; height: 16px;' } : undefined,
                                mods: Object.assign({}, obj.mods, { size: size })
                            },
                            {
                                elem: 'caption',
                                content: obj.st
                            }
                        ]
                    };
                }
            });
        })
    }
}
```

<a name="mods-direction"></a>

#### Модификатор `direction`

Задает направление для иконки-стрелки (`_type_arrow` и `_glyph_type-arrow`).

Допустимые значения: `'left'`, `'top'`, `'right'`, `'bottom'` (используется по умолчанию).

Способы установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-area',
    content: {
        block: 'x-table',
        xhead: [''].concat(['left', 'top', 'right', 'bottom']),
        yhead: [''].concat(['_type_arrow', '_glyph_type-arrow']),
        body: [
                { name: 'type', mods: { type: 'arrow' } },
                { name: 'glyph', mods: { glyph: 'type-arrow' } }
            ].map(function(obj) {
            return ['left', 'top', 'right', 'bottom'].map(function(direction) {
                return {
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    content: {
                        block: 'icon',
                        attrs: obj.name === 'type' ? { style: 'width: 16px; height: 16px;' } : undefined,
                        mods: Object.assign({}, obj.mods, { direction: direction } )
                    }
                };
            });
        })
    }
}
```

<a name="mods-action"></a>

#### Модификатор `action`

Определяет иконки-действия.

Допустимые значения: `'filter'`, `'settings'`, `'tableau'`.

Способы установки: `BEMJSON`, `JS`.

```js
[
    {
        block: 'x-table',
        head: ['filter', 'settings', 'tableau'],
        body: [
            ['filter', 'settings', 'tableau'].map(function(action) {
                return {
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    content: {
                        block: 'icon',
                        attrs: { style: 'width: 28px; height: 28px;' },
                        mods: { action: action }
                    }
                };
            })
        ]
    }
]
```

<a name="mods-glyph"></a>

#### Модификатор `glyph`

Определяет инлайновые SVG-иконки.

Допустимые значения: `'carets'`, `'type-arrow'`, `'type-check'`, `'type-close'`, `'type-cross'`, `'type-filter'`, `'type-tick'`, `'x-sign'`.

Способы установки: `BEMJSON`, `JS`.

```js
[
    {
        block: 'x-table',
        head: ['carets-v', 'type-arrow', 'type-check', 'type-close', 'type-cross', 'type-filter', 'type-tick', 'x-sign'],
        body: [
            ['carets-v', 'type-arrow', 'type-check', 'type-close', 'type-cross', 'type-filter', 'type-tick', 'x-sign'].map(function(glyph) {
                return {
                    block: 'x-area',
                    mods: { bordered: 'yes' },
                    content: {
                        block: 'icon',
                        mods: Object.assign({}, glyph === 'x-sign' ? { size: 's' } : {}, { glyph: glyph })
                    }
                };
            })
        ]
    }
]
```

### Поля блока

<a name="field-url"></a>

#### Поле `url`

Определяет адрес иконки.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['Поле url'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes' },
            content: {
                block: 'icon',
                attrs: { style: 'width:13px; height:21px' },
                url: '../../../examples.blocks/icon/_service/icon_service.assets/maps.svg'
            }
        }
    ]
}
```
