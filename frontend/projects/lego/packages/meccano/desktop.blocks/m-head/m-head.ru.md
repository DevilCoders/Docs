Шапка для интранет сервисов.

Хорошо отображается только в браузерах, полноценно поддерживающих `flexbox`.

* [Примеры использования](#Примеры-использования)
* [Модификаторы блока](#Модификаторы-блока)
* [Поля блока](#Поля-блока)
* [Вспомогательные блоки](#Вспомогательные-блоки)
* [Где используется](#Где-используется)

## Примеры использования

* [Минимальный набор параметров](#Минимальный-набор-параметров)
* [Настроить выпадающий список сервисов](#Настроить-выпадающий-список-сервисов)
* [Настроить меню шапки](#Настроить-меню-шапки)
* [Добавить кнопку основного действия](#Добавить-кнопку-основного-действия)
* [Настроить поисковую строку](#Настроить-поисковую-строку)
* [Отключить блок мессенджера](#Отключить-блок-мессенджера)
* [Настроить ссылки пользователя](#Настроить-ссылки-пользователя)

Еще посмотрите [ссылки на примеры](#Где-используется) использования в сервисах.

### Минимальный набор параметров

Чтобы собрать шапку, задайте тип оформления (модификатор [`type`](#type)), укажите название сервиса (`title`) и логин пользователя (`user`):

```js
{
    block: 'm-head',
    mods: { type: 'staff' },
    title: 'Империя',
    user: 'imperator'
}
```

Чтобы настроить цвет стрелки и оформление шапки, реализуйте свое значение модификатора [`type`](#type). [Вот пример](https://nda.ya.ru/3UZ4AQ), как это сделано в Вики.

### Настроить выпадающий список сервисов

Если нажать на стрелку в шапке, вы увидите выпадающий список с сервисами интранета.

Чтобы выделить свой сервис в этом списке, передайте его идентификатор в поле `service`. Значение должно совпадать c полем `application_id` в ответе от ручки `staff.yandex-team.ru/navigation-api/`.

Нажмите на стрелку в этом примере и вы увидите, что сервис `Стафф` выделен.

```js
{
    block: 'm-head',
    mods: { type: 'staff' },
    title: 'Стафф',
    user: 'imperator',
    service: 'staff'
}
```

Если вашего сервиса нет в списке, вы можете задать свою ссылку для формирования списка в поле `navigationApiHost`. Например, укажите https://staff.test.yandex-team.ru/navigation-api/, чтобы получить список сервисов со ссылками в тестовые ручки:

```js
{
    block: 'm-head',
    mods: { type: 'staff' },
    title: 'Стафф',
    user: 'imperator',
    service: 'staff',
    navigationApiHost: 'https://staff.test.yandex-team.ru/navigation-api/'
}
```

### Настроить меню шапки

Сделайте дополнительные ссылки на страницы вашего сервиса с помощью меню справа от стрелки. Пункты меню передайте в массиве `menuItems` ([список полей](#menuItem)). Чтобы отметить, что сейчас пользователь находится на одной из страниц в этом меню, укажите для этого пункта `current: 'yes'`.

Для каждого пункта меню вы можете настроить модификаторы, которые будут переданы в блок [`link`](https://github.yandex-team.ru/lego/islands/tree/dev/common.blocks/link):

```js
{
    block: 'm-head',
    mods: { type: 'staff' },
    title: 'Империя',
    user: 'imperator',
    menuItems: [
        { name: 'Татуин', url: '#' },
        { name: 'Корусант', url: '#', current: 'yes' },
        { name: 'Звезда Смерти', url: '#',  mods: { theme: 'strong' } }
    ]
}
```

Каждый пункт меню можно сделать выпадающим списком с подпунктами с помощью поля `subs`:

```js
{
    block: 'm-head',
    mods: { type: 'staff' },
    title: 'Империя',
    user: 'imperator',
    menuItems: [
        { name: 'Татуин', url: '#' },
        { name: 'Корусант', url: '#', current: 'yes' },
        {
            name: 'Звезда Смерти',
            subs: [
                { name: 'Первая Звезда Смерти', url: '#' },
                { name: 'Вторая Звезда Смерти', url: '#' }
            ]
        }
    ]
}
```

Если пунктов меню первого уровня слишком много, вы можете скрыть остальные под кнопкой с троеточием. Для этого укажите `more: 'yes'`, а в `subs` передайте остальные пункты меню. `name` и `url` в этом случае не указывайте:

```js
{
    block: 'm-head',
    mods: { type: 'staff' },
    title: 'Империя',
    user: 'imperator',
    menuItems: [
        {  name: 'Татуин', url: '#' },
        {  name: 'Корусант', url: '#', current: 'yes' },
        {
            more: 'yes',
            subs: [
                { name: 'Первая Звезда Смерти', url: '#' },
                { name: 'Вторая звезда Смерти', url: '#' }
            ]
        }
    ]
}
```

### Добавить кнопку основного действия

Чтобы добавить кнопку основного действия, используйте поле `action`:

```js
{
    block: 'm-head',
    mods: { type: 'staff' },
    title: 'Империя',
    user: 'imperator',
    action: 'Уничтожить'
}
```

Чтобы сделать кнопку ссылкой, передайте в `action` [объект](#action) с полями `url` и `content`:

```js
{
    block: 'm-head',
    mods: { type: 'staff' },
    title: 'Империя',
    user: 'imperator',
    action: {
        url: 'https://yandex.ru',
        content: 'Уничтожить'
    }
}
```

Чтобы добавить выпадающий список с дополнительными кнопками, передайте список в поле `items`:

```js
{
    block: 'm-head',
    mods: { type: 'staff' },
    title: 'Империя',
    user: 'imperator',
    action: {
        url: 'https://yandex.ru',
        content: 'Уничтожить',
        items: [
            { url: '#', name: 'Распустить сенат' },
            { url: '#', name: 'Уничтожить джедаев' },
            { url: '#', name: 'Уничтожить повстанцев', mods: { disabled: 'yes' } }
        ]
    }
}
```

### Настроить поисковую строку

Чтобы добавить поисковую строку, укажите `search: true`. По умолчанию добавляется [поиск по всем сервисам](https://search.yandex-team.ru/search):

```js
{
    block: 'm-head',
    mods: { type: 'staff' },
    title: 'Империя',
    user: 'imperator',
    search: true
}
```

В поле `search` вы можете передать объект с [параметрами поисковой строки](#search). Например, укажите, какой поиск надо использовать, передав его адрес в поле `action`:

```js
{
    block: 'm-head',
    mods: { type: 'staff' },
    title: 'Империя',
    user: 'imperator',
    search: {
        hint: 'Найти джедаев',
        action: '//search.yandex-team.ru/peoplesearch'
    }
}
```

### Отключить блок мессенджера

Блок мессенджера добавляется в шапку по умолчанию. Если он вам не нужен, отключите его, указав `messenger: false`:


```js
{
    block: 'm-head',
    mods: { type: 'staff' },
    title: 'Империя',
    user: 'imperator',
    messenger: false
}
```

### Настроить ссылки пользователя

При нажатии на фото пользователя появляется выпадающий список со ссылками. Настройте эти ссылки с помощью поля [`customUserLinks`](#customUserLinks):

```js
{
    block: 'm-head',
    mods: { type: 'staff' },
    title: 'Империя',
    user: 'imperator',
    messenger: false,
    customUserLinks: {
        my: {
            url: 'https://staff.yandex-team.ru/imperator',
            text: 'Императорская'
        },
        settings: {
            url: 'https://staff.yandex-team.ru/settings/',
            text: 'Мои настройки'
        }
    }
}
```

## Модификаторы блока

### `type`

Используйте модификатор `type`, чтобы задать настройки оформления шапки на уровне сервиса.

**Возможные значения:**

`staff` — делает оформление шапки таким же, как на https://staff.yandex-team.ru.

В некоторых сервисах реализуются свои значения модификатора с настройками оформления, например в [Трекере](https://st.yandex-team.ru/) стрелка синяя, и отступы между элементами шапки изменены. [См. другие примеры сервисов](#Где-используется), использующих шапку.

## Поля блока

![Поля m-head](https://jing.yandex-team.ru/files/migelle/m-head-fields.png)

Поле | Тип | Описание
-----|-----|-----
`title` | `String` | Название сервиса, которое указывается в стрелке. По умолчанию `Service Name`.
`user` | `String` | Логин пользователя на стаффе. Обязательный параметр, т.к. сервисы в интранете не должны работать для неавторизованного пользователя.
[`customUserLinks`](#customUserLinks) | `Object` | Настройка ссылок в выпадающем списке при нажатии на фото пользователя. <br>Если не указано, то будут использованы стандартные ссылки: [Я на Стаффе](https://staff.yandex-team.ru), [Настройки](https://staff.yandex-team.ru/settings/).
`service` | `String` | ID сервиса. Используется для выделения текущего сервиса в выпадающем списке сервисов.<br>Значение должно совпадать c полем `application_id` в ответе от ручки, указанной в `navigationApiHost`.
`navigationApiHost` | `String` | Ссылка на список сервисов для создания выпадающего списка при нажатии на стрелку. По умолчанию:<br>`https://staff.yandex-team.ru/navigation-api/`<br>Укажите `https://staff.test.yandex-team.ru/navigation-api/`, чтобы получить список сервисов со ссылками в тестовые ручки.<br>Полученный список сервисов кэшируется на сутки в `localStorage`.
[`menuItems`](#menuItem) | `Array<menuItem>` | Меню шапки. Каждый пункт меню это ссылка или выпадающий список.
`action` | `String\|Object` | Кнопка основного действия в шапке, например в Трекере это кнопка К. Если `String`, то будет создана кнопка с указанной строкой. Если `Object`, то кнопка будет ссылкой, а рядом с кнопкой можно создать выпадающий список с дополнительными кнопками.
[`search`](#search) | `Boolean\|Object` | Настройки поисковой строки в шапке.<br>Если `false` или не задано, поисковой строки в шапке не будет.<br>Если `true` — то будет использован поиск по всем сервисам: https://search.yandex-team.ru/search
[`messenger`](https://github.yandex-team.ru/lego/islands/tree/dev/contribs/messenger) | `false\|Object` | Добавляет кнопку [мессенджера](https://q.yandex-team.ru) с модификатором `internal: 'yes'`. Если значение не передано, будет добавлен мессенджер с параметрами по умолчанию. [Подробнее в документации контриба messenger](https://github.yandex-team.ru/lego/islands/tree/dev/contribs/messenger).<br>Если мессенджер не нужен, передайте `false`.
[`notifier`](https://github.yandex-team.ru/lego/islands/tree/dev/contribs/notifier) | `Object` | Добавляет блок центра уведомлений (колокол) с модификатором `size: 'm'` . [Подробнее в документации контриба notifier](https://github.yandex-team.ru/lego/islands/tree/dev/contribs/notifier), а также [см. пример](https://github.yandex-team.ru/tools/yandex-wiki-www/blob/dcec15b6b8de47d7d6e360d5b9e68325ede18167/blocks/desktop.blocks/intranet/desktop.blocks/b-head/b-head.bemtree.js#L42) использования уведомлений в Вики.

### action

Кнопка основного действия в шапке (`m-head-action`).

![Пример кнопки в Этушке](https://jing.yandex-team.ru/files/migelle/m-head-action.png)

Поле | Тип | Описание
-----|-----|-----
`url` | `String` | Ссылка, которая откроется по нажатию на кнопку.
`content` | `String` | Текст кнопки.
[`items`](#actionItem) | `Array<actionItem>` | Выпадающий список с дополнительными ссылками.

### actionItem

Дополнительная кнопка. Это ссылка из выпадающего списка рядом с [кнопкой основного действия](#action).

Поле | Тип | Описание
-----|-----|-----
`url` | `String` | Ссылка, которая откроется по нажатию на кнопку.
`name` | `String` | Текст кнопки.
`mods` | `{ modName: 'modVal' }` | Модификаторы, которые будут переданы в блок [`link`](https://github.yandex-team.ru/lego/islands/tree/dev/common.blocks/link) для этого элемента списка.
`mix` |  `{ block: blockName }` | Миксы, которые будут переданы в блок [`link`](https://github.yandex-team.ru/lego/islands/tree/dev/common.blocks/link) для этого элемента списка.

### customUserLinks

Объект настройки ссылок из выпадающего списка (`m-head-services`) при нажатии на фото пользователя (`m-head-user`). Ссылку `Выход` настроить нельзя, она добавляется автоматически.

![Поля customUserLinks](https://jing.yandex-team.ru/files/migelle/m-head-customUserLinks.png)

Поле | Тип | Описание
-----|-----|-----
`my` | `{ url: String, text: String}` | Ссылка на страницу пользователя. По умолчанию:<br>`{ url: '//staff.yandex-team.ru/', text: BEM.I18N('m-head-user', 'staff')}`
`settings` | `{ url: String, text: String}` | Ссылка на страницу с настройками сервиса. По умолчанию:<br>`{ url: '//staff.yandex-team.ru/settings/', text: BEM.I18N('m-head-user', 'options')}`

### menuItem

Пункт меню в шапке (`m-head-menu__item`). Может содержать вложенные пункты меню.

Поле | Тип | Описание
-----|-----|-----
`name` | `String` | Название пункта меню.
`url` | `String` | Адрес ссылки для этого пункта меню.
`mods` | `{ modName: 'modVal' }` | Модификаторы, которые будут переданы в блок [`link`](https://github.yandex-team.ru/lego/islands/tree/dev/common.blocks/link) для этого элемента списка.
`current` | `String='yes'` | Флаг, выделяющий текущий пункт меню. Используйте этот флаг, чтобы показать, на какой странице находится пользователь.
`subs` | `Array<menuItem>` | Выпадающий список подпунктов. Сейчас подпункт не может иметь вложенный список пунктов ([тикет на исправление](https://nda.ya.ru/3UYuzL)), поэтому не используйте `subs` внутри `subs`.
`more` | `String='yes'` | Флаг, добавляющий троеточие с выпадающим списком пунктов меню, указанных в `subs`.<br>Не задавайте поля `name` и `url` в объекте с этим флагом.

### search

Поисковая строка в шапке. Используется для поиска по интранету или по отдельным сервисам.

![Пример поисковой строки на стаффе](https://jing.yandex-team.ru/files/migelle/m-head-search.png)

Поле | Тип | Описание
-----|-----|-----
`hint` | `String` | Текст для подсказки (placeholder) в поисковой строке. По умолчанию `поиск по интранету`.
`action` | `String` | Ссылка на раздел поиска по интранету. По умолчанию:<br>`https://search.yandex-team.ru/search`.
`autocomplete` | `Boolean` | Если `false`, то выключает поисковые подсказки (suggest). По умолчанию `true`.
`formParams` | `Object` | Объект, содержащий GET-параметры поисковой формы при её отправке, например `{  opensearch: "1"}`

## Вспомогательные блоки

Эти блоки используются только в блоке `m-head`:

* [`m-head-arrow`](../m-head-arrow) — стрелка в шапке.
* [`m-head-menu`](../m-head-menu) — меню шапки. Каждый пункт меню — это элементы блока: `m-head-menu__item`
* [`m-head-action`](../m-head-action) — кнопка основного действия в шапке.
* [`m-head-search`](../m-head-search) — строка поиска с кнопкой "Найти".
* [`m-head-user`](../m-head-user) — фотография пользователя.
* [`m-head-services`](../m-head-services) — выпадающий список ссылок, появляющийся при нажатии на стрелку (`m-head-arrow`) или фото пользователя (`m-head-user`).

## Где используется

* [Внутренний поиск](https://search.yandex-team.ru/search) — [пример кода](https://github.yandex-team.ru/tools/intrasearch-www/blob/1cc2b70398e00b4c6ab0003eed416f484b4cceb7/desktop.blocks/head/head.bemhtml.js#L39).
* [Стафф](https://staff.yandex-team.ru) — [пример кода](https://github.yandex-team.ru/tools/staff-www/blob/d8dcaf03f958c742d0f5924dc4181dcb6c58fd6c/blocks/desktop/staff-page/__head/staff-page__head.bemhtml.js#L6).
* [Вики](https://wiki.yandex-team.ru) — [пример кода](https://github.yandex-team.ru/tools/yandex-wiki-www/blob/dcec15b6b8de47d7d6e360d5b9e68325ede18167/blocks/desktop.blocks/intranet/desktop.blocks/b-head/b-head.bemtree.js#L3).
* [Трекер](https://st.yandex-team.ru/agile/board/84) — [пример кода](https://github.yandex-team.ru/tools/startrek-www/blob/a67fafa97866d6f5099472ba6a9d735d746820b8/blocks-desktop/m-head/_type/m-head_type_startrek.priv.js#L7).
* [Этушка](https://my.at.yandex-team.ru) — [пример кода](https://github.yandex-team.ru/tools/atushka-frontend/blob/06fe1ac8eb871b14fb397644ed3286d00d5dc5d0/static/islands/desktop.bundles/index/index.bemdecl.js#L11).