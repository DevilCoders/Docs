# ticker

Счетчик количества новых уведомлений. Может располагаться не только в блоке [User2](../user2/user2.ru.md).

При количестве уведомлений:

- меньше 9 — отображается в виде круга (MSIE ниже 9 — прямоугольник).
- 9+ — отображается в виде овала.

Также можно задать максимальное количество уведомлений [`maxCount`](#field-maxсount) для показа на странице. При достижении максимального значения, счетчик перестанет увеличиваться.

## Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [state](#mods-state)| `'normal'`, `'empty'` | `BEMJSON`, `JS` | Скрытие блока. |

req — обязательный модификатор.

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [count](#field-count) | `Number` | Фактическое количество уведомлений. |
| [maxCount](#field-maxсount) | `Number` | Максимальное количество уведомлений. По умолчанию — 99. |
| [url](#field-url) | `String` | Адрес. |

### Элементы блока

| Элемент | Описание |
| ------- | -------- |
| [count](#elem-count) | Количество уведомлений. Обертка для элементов `text` и `value`. |
| [text](#elem-text) | Скрытый текст для программ экранного доступа. |
| [value](#elem-value) | Количество уведомлений, которое будет показано пользователю. |

## Подробное описание

### Модификаторы блока

<a name="mods-state"></a>

#### Модификатор `state`

Отвечает за скрытие блока, если нет новых уведомлений.

Допустимое значение: `'normal'`, `'empty'`.

Способы установки: `BEMJSON`, `JS`.

> **Примечание.** Значение модификатора можно изменять программно.

```js
{
    block: 'x-table',
    head: ['_state_normal', '_state_empty'],
    body: [
        {
            block: 'ticker',
            mods: { state: 'normal' },
            count: 13
        },
        {
            block: 'ticker',
            mods: { state: 'empty' },
            count: 13
        }
    ]
}
```

### Поля блока

<a name="field-count"></a>

#### Поле `count`

Определяет фактическое количество уведомлений.

Тип: `Number`.

```js
{
    block: 'x-table',
    head: ['count = 13'],
    body: [
        {
            block: 'ticker',
            count: 13
        }
    ]
}
```

<a name="field-maxсount"></a>

#### Поле `maxCount`

Определяет максимальное количество уведомлений. По умолчанию — 99.

Если:

* `count` > `maxCount` — отображается значение поля `maxCount`;
* `count` < `maxCount` — отображается значение поля `count`.

Тип: `Number`.

```js
{
    block: 'x-table',
    head: ['count = 13, maxCount = 7', 'count = 7, maxCount = 13'],
    body: [
        {
            block: 'ticker',
            count: 13,
            url: '#',
            maxCount: 7
        },
        {
            block: 'ticker',
            count: 7,
            maxCount: 13
        }
    ]
}
```

<a name="field-url"></a>

#### Поле `url`

Определяет адрес, по которому осуществляется переход при нажатии на блок.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['Поле url'],
    body: [
        {
            block: 'ticker',
            count: 13,
             url: 'https://lego.yandex-team.ru/',
        }
    ]
}
```

### Элементы блока

<a name="elem-count"></a>

#### Элемент `count`

Определяет количество уведомлений.  Обертка для элементов `text` и `value`.

- Если не задано поле `url`, в HTML выражен тегом `<span>`:

    ```html
    <span class="ticker__count ticker__plain">
        <span class="ticker__text a11y-hidden">Уведомлений</span>
        <span class="ticker__value" title="13">13</span>
    </span>
    ```

- Если задано поле `url`, в HTML выражен тегом `<a>`:

    ```html
    <a class="ticker__count" href="https://lego.yandex-team.ru/">
        <span class="ticker__text a11y-hidden">Уведомлений</span>
        <span class="ticker__value" title="13">13</span>
    </a>
    ```

<a name="elem-text"></a>

#### Элемент `text`

Определяет скрытый текст. По умолчанию — «Уведомлений». Нужен для программ экранного доступа. В шаблоне элемента выполняется примешивание блока [a11-hidden](../a11y-hidden/a11y-hidden.ru.md), в котором можно задать альтернативный текст для программ экранного доступа.

В HTML выражен тегом `<span>`:

```html
<span class="ticker__text a11y-hidden">Уведомлений</span>
```

Для элемента `text` нужно гарантировать подключение следующих зависимостей:

```js
{
    mustDeps: [
        { block: 'i-bem', elems: ['html', 'i18n'] }
    ],
    shouldDeps: [
        { block: 'a11y-hidden' }
    ]
}
```

<a name="elem-value"></a>

#### Элемент `value`

Определяет количество уведомлений, которое будет показано пользователю. Также содержит подсказку (атрибут `title`) с фактическим количеством новых уведомлений.

- `count` = 13, `maxCount` = 7:

    ```html
    <span class="ticker__value" title="13">7</span>
    ```

- `count` = 7, `maxCount` = 13:

    ```html
    <span class="ticker__value" title="7">7</span>
    ```
