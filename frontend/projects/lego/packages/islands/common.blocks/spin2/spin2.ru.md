# spin2

Используется для создания индикатора загрузки. Иллюстрирует ход выполнения процесса.

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [position](#mods-position)| `center` | `BEMJSON`, `JS` | Позиционирование индикатора загрузки. |
| [progress](#mods-progress) | `yes` | `BEMJSON`, `JS` | Отображает/скрывает индикатор загрузки. |
| [size](#mods-size) (req) | `xxs`, `xs`, `s`, `m`, `l` | `BEMJSON`, `JS` | Размер индикатора загрузки. |
| [tone](#mods-tone) | `blue`, `dark`, `default`, `grey`, `market`, `red` | `BEMJSON`, `JS` | Цветовой тон индикатора загрузки. |
| [view](#mods-view) | `default`  | `BEMJSON`, `JS` | Вид индикатора загрузки. |

req — обязательный модификатор.

## Подробное описание

### Модификаторы блока

<a name="mods-position"></a>

#### Модификатор `position`

Позиционирует индикатор загрузки по центру.

Допустимые значения: `center`.

Способ установки: `BEMJSON`, `JS`.

> **Важно!** Необходимо использовать с модификатором `progress`.

```js
[
    ['xxs', 'xs', 's', 'm', 'l'].map(function(size) {
        return {
            block: 'example',
            attrs: { style: 'position: relative; display: inline-block; width: 42px; height: 42px; margin: 4px; padding: 0; border: 1px solid #bbb;' },
            mods: { position: 'related' },
            content: {
                block: 'spin2',
                mods: { size: size, progress: 'yes', position: 'center' }
            }
        };
    })
]
```

<a name="mods-progress"></a>

#### Модификатор `progress`

Отображает/скрывает индикатор загрузки.

Допустимые значения: `yes`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['yes', ''],
    body: [
        ['yes', ''].map(function(progress) {
            return {
                block: 'example',
                attrs: { style: 'position: relative; display: inline-block; width: 42px; height: 42px; margin: 4px; padding: 0; border: 1px solid #bbb;' },
                mods: { position: 'related' },
                content: {
                    block: 'spin2',
                    mods: { size: 'm', progress: progress, position: 'center' }
                }
            };
        })
    ]
}
```

<a name="mods-size"></a>

#### Модификатор `size`

Определяет размер индикатора загрузки. **Обязательный**.

Допустимые значения: `xxs`, `xs`, `s`, `m`, `l`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['xxs', 'xs', 's', 'm', 'l'],
    body: [
        ['xxs', 'xs', 's', 'm', 'l'].map(function(size) {
            return {
                block: 'spin2',
                mods: { progress: 'yes', size: size }
            };
        })
    ]
}
```

<a name="mods-tone"></a>

#### Модификатор `tone`

Определяет цветовой тон индикатора загрузки.

Допустимые значения: `blue`, `dark`, `default`, `grey`, `market`, `red`.

Способ установки: `BEMJSON`, `JS`.

> **Важно!** Необходимо использовать с модификатором `view`.

```js
{
    block: 'x-table',
    head: ['blue', 'dark', 'default', 'grey', 'market', 'red'],
    body: [
        ['blue', 'dark', 'default', 'grey', 'market', 'red'].map(function(tone) {
            return {
                block: 'example',
                attrs: { style: 'position: relative; display: inline-block; width: 42px; height: 42px; margin: 4px; padding: 0; border: 1px solid #bbb;' },
                mods: {
                    position: 'related'
                },
                mix: { block: 'toner', mods: { tone, view: 'default' } },
                content: {
                    block: 'spin2',
                    mods: {
                        tone,
                        size: 'm',
                        view: 'default',
                        progress: 'yes',
                        position: 'center'
                    }
                }
            };
        })
    ]
}
```

<a name="mods-view"></a>

#### Модификатор `view`

Определяет вид индикатора загрузки.

Допустимые значения: `default`.

Способ установки: `BEMJSON`, `JS`.

> **Важно!** Необходимо использовать с модификатором `tone`.

```js
{
    block: 'spin2',
    mods: {
        tone: 'default',
        size: 'm',
        view: 'default',
        progress: 'yes',
        position: 'center'
    }
}
```