# tumbler

Используется для создания переключателей (тумблеров).

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [theme](#mods-theme) (req)| `'normal'`, `'tiny'`| `BEMJSON`, `JS` | Стилевое оформление. |
| [size](#mods-size) (req)| `'xs'`, `'s'`, `'n'`, `'m'` | Размер. |
| [view](#mods-view) | `'default'`, `'classic'` | `BEMJSON`, `JS` | Вид. |
| [tone](#mods-tone) | `'default'`, `'red'`, `'grey'`, `'dark'` | `BEMJSON`, `JS` | Цветовой тон. |
| [disabled](#mods-disabled) | `'yes'` | `BEMJSON`, `JS` | Неактивное состояние. |

req — обязательный модификатор.

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [content](#field-content) | `BEMJSON` | Определяет атрибуты правой и левой метки тумблера. Опциональное поле. |
| [name](#field-name) | `String` | Уникальное имя блока. Опциональное поле.
| [title](#field-title) | `String` | Текст всплывающей подсказки. |
| [attrs](#field-attrs) | `BEMJSON` | Произвольные атрибуты тумблера. |

## Подробное описание

### Модификаторы блока

<a name="mods-theme"></a>

#### Модификатор `theme`

Устанавливает стилевое оформление тумблера. **Обязательный**.

Допустимые значения: `'normal'`, `'tiny'`.

Способ установки: `BEMJSON`, `JS`.

<a name="theme-normal"></a>

**Обычный тумблер (модификатор `theme` в значении `normal`)**

Используется в большинстве случаев.

```js
{
    block: 'tumbler',
    mods: { size: 'm', theme: 'normal' }, 
}
```

<a name="theme-tiny"></a>

**Миниатюрный тумблер (модификатор `theme` в значении `tiny`)**

Используется для изменения внешнего вида блока, чтобы сделать тумблер менее заметным на странице.

```js
{
    block: 'tumbler',
    mods: { size: 'm', theme: 'tiny' }, 
}
```

<a name="mods-size"></a>

#### Модификатор `size`

Задает размер тумблера. **Обязательный**.

Допустимые значения: `'xs'`, `'s'`, `'n'`, `'m'` .

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'x-table',
    head: ['xs', 's', 'm', 'n'],
    body: [
        ['xs', 's', 'm', 'n'].map((size) => {
            return {
                block: 'tumbler',
                mods: { theme: 'normal', size: size }
            };
        })
    ]
}
```

<a name="mods-view"></a>

#### Модификатор `view`

Задает вид тумблера.

Допустимые значения: `'default'`, `'classic'`.

Способ установки: `BEMJSON`, `JS`.

> **Важно!** Модификатор `view` в значении `default` необходимо использовать с модификатором `tone`.

```js
{
    block: 'x-table',
    head: ['default', 'classic'],
    body: [
        ['default', 'classic'].map(function(view) {
            return {
                block: 'tumbler',
                mods: { theme: 'normal', size: 'm', view: view, tone: 'default' }
            };
        })
    ]
}
```

<a name="mods-tone"></a>

#### Модификатор `tone`

Задает тон тумблера.

Допустимые значения: `'default'`, `'red'`, `'grey'`, `'dark'`, `'market'`.

Способ установки: `BEMJSON`, `JS`.

> **Важно!** Необходимо использовать с модификатором `view` в значении `default`.

```js
{
    block: 'x-table',
    head: ['default', 'red', 'grey', 'dark'],
    body: [
        ['default', 'red', 'grey', 'dark'].map(function(tone) {
            return {
                block: 'tumbler',
                mods: { theme: 'normal', size: 'm', view: 'default', tone: tone }
            };
        })
    ]
}
```

<a name="mods-disabled"></a>

#### Модификатор `disabled`

Отвечает за неактивное состояние, при котором тумблер виден, но недоступен для действий пользователя.

Нельзя:

* установить модификаторы `checked`, `focused` и `hovered` (существующие удаляются);
* вызвать БЭМ-события.

Допустимое значение: `'yes'`.

Способы установки: `BEMJSON`, `JS`.

> **Примечание.** Неактивное состояние блока можно изменять программно.

```js
{
    block: 'x-table',
    head: ['_disabled'],
    body: [
        {
            block: 'tumbler',
            mods: { theme: 'normal', size: 'm', disabled: 'yes' }
        }
    ]
}
```

### Поля блока

<a name="field-content"></a>

#### Поле `content`

Определяет атрибуты правой и левой метки тумблера. Опциональное поле.

Тип: `BEMJSON`.

```js
{
	block: 'tumbler',
	mods: { theme: 'normal', size: 'm' },
	content: [
		{
    		elem: 'option',
        	side: 'left',
        	content: 'Подпись слева',
        	value: 'gray'
		},
		{
    		elem: 'option',
        	side: 'right',
        	content: 'Подпись справа',
        	value: 'gray'
    	}
    ]
}
```

<a name="field-name"></a>

#### Поле `name`

Определяет уникальное имя элемента блока `tumbler__input`. Если не указано, то значение генерируется автоматически.

Тип: `String`.

```js
{
    block: 'tumbler',
	mods: { size: 'm', theme: 'normal' },
	name: 'my-tumbler'
}
```

<a name="field-title"></a>

#### Поле `title`

Определяет содержание всплывающей подсказки.

Тип: `String`.

> **Примечание.** Вид такой подсказки зависит от браузера, настроек операционной системы и не может быть изменен с помощью HTML-кода или стилей.

```js
{
    block: 'tumbler',
	mods: { size: 'm', theme: 'normal' },
	title: 'My tumbler'
}
```

<a name="field-attrs"></a>

#### Поле `attrs`

Определяет произвольные атрибуты тумблера.

Тип: `BEMJSON`.

```js
{
    block: 'x-table',
    head: ['Поле attrs'],
    body: [
        {
            block: 'tumbler',
			mods: { theme: 'normal' , size: 'm' },
            attrs: { style: 'color: red;' }
        }
    ]
}
```