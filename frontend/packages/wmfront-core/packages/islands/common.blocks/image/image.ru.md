# image

Используется для вставки изображений.

## Обзор

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [url](#field-url) | `String` | Адрес изображения. |
| [alt](#field-alt) | `String` | Альтернативный текст для изображения. |
| [width](#field-width) | `Number`, `String` | Ширина изображения. |
| [height](#field-height) | `Number`, `String` | Высота изображения. |

## Подробное описание

### Поля блока

<a name="field-url"></a>

#### Поле `url`

Определяет адрес изображения.

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
                block: 'image',
                url: '../../../examples.blocks/image/image.assets/girl.png'
            }
        }
    ]
}
```

<a name="field-alt"></a>

#### Поле `alt`

Определяет альтернативный текст для изображения.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['Поле alt'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes' },
            content: {
                block: 'image',
                alt: 'Emily Ratajkowski',
                url: '../../../examples.blocks/image/image.assets/girl.png'
            }
        }
    ]
}
```

<a name="field-width"></a>

#### Поле `width`

Определяет ширину изображения.

Тип: `Number`, `String`.

```js
{
    block: 'x-table',
    head: ['Поле width'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes' },
            content: {
                block: 'image',
                width: 200,
                url: '../../../examples.blocks/image/image.assets/girl.png'
            }
        }
    ]
}
```

<a name="field-height"></a>

#### Поле `height`

Определяет высоту изображения.

Тип: `Number`, `String`.

```js
{
    block: 'x-table',
    head: ['Поле height'],
    body: [
        {
            block: 'x-area',
            mods: { bordered: 'yes' },
            content: {
                block: 'image',
                height: 200,
                url: '../../../examples.blocks/image/image.assets/girl.png'
            }
        }
    ]
}
```
