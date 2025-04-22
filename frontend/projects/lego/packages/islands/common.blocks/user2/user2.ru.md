# user2

Используется для отображения блока пользователя в правом верхнем углу страницы.

> **Важно!** Стили блока следует добавлять одним из двух способов:
> используя блок `user2` внутри блока `b-page`. Этот блок содержит стили для корректной работы `user2`.
> вручную добавив стили из `b-page` для `body`. В частности, в iOS если не проставить на `body` стили `cursor:pointer`, то никаких событий не будет и клики вне попапа обрабатываться не будут.

# Обзор

### Модификаторы блока

| Модификатор | Допустимые значения | Способы установки | Описание |
| ----------- | ------------------- | ----------------- | -------- |
| [fetch-accounts](#mods-fetch-accounts) | `yes` | `BEMJSON`, `JS` | Отображение аккаунтов пользователя. |
| [fetch-counters](#mods-fetch-counters)| `yes` | `BEMJSON`, `JS` | Отображение количества непрочитанных писем для всех аккаунтов пользователя. |
| [fetch-unread](#mods-fetch-unread)| `yes` | `BEMJSON`, `JS` | Отображение количества непрочитанных писем для текущего аккаунта пользователя. |
| [has-hat](#mods-has-hat) | `yes` | `BEMJSON` | Отображение баннера. |
| [provider](#mods-provider) | `yandex-team` | `BEMJSON` | Провайдер данных об аккаунтах пользователя. |
| [has-logout](#mods-has-logout) | `yes` | `BEMJSON` | Наличие у аккаунтов крестика для выхода из системы. |
| [with-organizations](#mods-with-organizations) | `yes` | `BEMJSON`, `JS` | Наличие блока организаций пользователя. |
| [fetch-organizations](#mods-fetch-organizations) | `yes` | `BEMJSON`, `JS` | ajax-загрузка организаций пользователя. |
| [with-pin-code](#mods-with-pin-code) | `yes` | `BEMJSON` | Наличие кнопки генерации Pin-кода. |

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [uid](#field-uid) | `Number` | Уникальный идентификатор пользователя. |
| [yu](#field-yu) | `Number` | Cookie-файлы `yandexuid`. |
| [yaplus](#field-yaplus) | `Boolean` | Наличие подписки Плюс у пользователя. |
| [hat](#field-hat) | `BEMJSON` | Объект баннера, встраиваемого в меню блока пользователя. |
| [retpath](#field-retpath) | `String` | URL страницы. |
| [avatarId](#field-avatarId) | `String` | Идентификатор аватарки пользователя. |
| [origin](#field-origin) | `String` | Название текущего сервиса с `user2`. |
| [camera](#field-camera) | `Boolean` | Наличие иконки фотоаппарата на стандартном аватаре в шапке выпадающего меню. |
| [name](#field-name) | `String` | Имя пользователя. |
| [maxLength](#field-maxLength) | `Number` | Максимальная видимая длина имени пользователя. |
| [unreadCount](#field-unreadCount) | `Number` | Количество видимых непрочитанных писем. |
| [passportHost](#field-passportHost) | `String` | URL страницы паспорта. |
| [source](#field-source) | `String` | Идентификатор сервиса. |
| [preset](#field-preset) | `String` | Предопределённый набор сервисов, используемых в организациях Коннекта. |
| [secretKey](#field-secretKey) | `String` | Секретный ключ. |

## Подробное описание

### Модификаторы блока

<a name="mods-fetch-accounts"></a>

#### Модификатор `fetch-accounts`

Отображает аккаунты пользователя.

> **Примечание.** Инициализируется через `accountsDataProvider`.

Допустимые значения: `yes`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    mods: {
        'fetch-accounts': 'yes'
    },
    uid: 6789054321,
    yu: 123456789012345678,
    retpath: 'https://yandex.ru',
    passportHost: 'https://passport.yandex.ru',
    name: 'Денис Кузнецов',
    js: {
        live: false,
        accountsDataProvider: 'accounts-mock-provider',
        mailCallerId: 'lego'
    }
}
```

<a name="mods-fetch-counters"></a>

#### Модификатор `fetch-counters`

Отображает количество непрочитанных писем всех аккаунтов пользователя.

> **Примечание.** Чтобы получить список непрочитанных писем сразу и при этом не обращаться к ручке дважды, можно отключить ленивую инициализацию блока.

Предоставляет публичный метод `updateCounters`. Метод принимает параметр `force` булевого типа, в значении `true` параметр форсирует отправление нового запроса.
В отличие от `_fetch-unread` забирает аккаунты из новой ручки, для использования которой необходимо передать идентификатор потребителя в качестве `JS`-параметра `mailCallerId`. Подробнее о том, как [получить идентификатор](https://wiki.yandex-team.ru/users/jkennedy/api2/)

Допустимые значения: `yes`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    mods: {
        'fetch-accounts': 'yes',
        'fetch-counters': 'yes'
    },
    yaplus: false,
    uid: 6789054321, // Для выхода
    yu: 123456789012345678, // Для выхода, смены пользователя, _fetch_accounts, _fetch_unread
    retpath: 'https://yandex.ru', // Для всего
    passportHost: 'https://passport.yandex.ru',
    unreadCount: 7,
    name: 'Денис Кузнецов',
    js: {
        live: false,
        accountsDataProvider: 'accounts-mock-provider',
        mailCallerId: 'lego'
    }
}
```

<a name="mods-fetch-unread"></a>

#### Модификатор `fetch-unread`

Отображает количество непрочитанных писем для текущего аккаунта пользователя.

> **Примечание.** Инициализируется через `unreadDataProvider`

Допустимые значения: `yes`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    yaplus: false,
    mods: {
        'fetch-unread': 'yes'
    },
    uid: 84473936,
    yu: 123456789012345678,
    retpath: 'https://yandex.ru',
    passportHost: 'https://passport.yandex.ru',
    name: 'Денис Кузнецов',
    unreadCount: 7
}
```

<a name="mods-has-hat"></a>

#### Модификатор `has-hat`

Определяет наличие баннера. При инициализации блока отправляет запрос за данными, из которых впоследствии формирует баннер. Необходимо использовать совместно с полем `hat`.

Допустимые значения: `yes`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    yaplus: false,
    mods: { 'has-hat': 'yes' },
    hat: {
        block: 'user-hat',
        fetchUrl: 'https://yabs.yandex.ru/page/280743',
        mods: { 'fetch-data': 'yes' }
    },
    uid: 84473936,
    yu: 123456789012345678,
    retpath: 'https://yandex.ru',
    passportHost: 'https://passport.yandex.ru',
    name: 'Денис Кузнецов'
}
```

<a name="mods-provider"></a>

#### Модификатор `provider`

Определяет провайдер данных об аккаунтах пользователя.

Допустимые значения: `yandex-team`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    mods: { provider: 'yandex-team' },
    uid: 123456789,
    yu: 123456789,
    retpath: 'https://yandex-team23123121.ru',
    passportHost: 'https://passport.yandex-team.ru',
    avatarHost: 'https://center.yandex-team.ru',
    name: 'Чак Норриc',
    avatarId: 'robot-serp-bot',
    accounts: [
        {
            block: 'user-account',
            mix: { block: 'user2', elem: 'account', js: { uid: 123456789 } },
            pic: { avatarId: 'robot-serptools' },
            name: 'WALL-E Bot'
        }
    ]
}
```

<a name="mods-has-logout"></a>

#### Модификатор `has-logout`

Добавляет в попап рядом с аккаунтами пользователя крестик для выхода из системы.

Допустимые значения: `yes`.

Способ установки: `BEMJSON`, `JS`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    mods: {
        'has-logout': 'yes',
        'fetch-accounts': 'yes'
    },
    yaplus: false,
    uid: 6789054321,
    yu: 123456789012345678,
    retpath: 'https://yandex.ru',
    passportHost: 'https://passport.yandex.ru',
    name: 'Денис Кузнецов',
    subname: 'denis.kuznecov@yandex.ru',
    js: {
        live: false,
        accountsDataProvider: 'accounts-mock-provider',
        mailCallerId: 'lego'
    }
}
```

<a name="field-uid"></a>

<a name="mods-with-organizations"></a>

#### Модификатор `with-organizations`

Наличие блока организаций пользователя.
Используется совместно с модификатором `fetch-organizations` либо передачей поля `organizations`.
Для использования блока организаций также необходимо передать поля `secretKey`, `source` и `preset`.
Если блок подключается не через установку модификатора `fetch-organizations`,
а посредством передачи поля `organizations`, то также необходимо передать поле `currentOrgId`.

Допустимые значения: `yes`.

Способ установки: `BEMJSON`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    mods: {
        'fetch-accounts': 'yes',
        'with-organizations': 'yes',
    },
    uid: 6789054321,
    yu: 123456789012345678,
    retpath: 'https://yandex.ru',
    passportHost: 'https://passport.yandex.ru',
    name: 'Денис Кузнецов',
    currentOrgId: 12345,
    organizations: {
        '6789054321': [
            {
                id: 12345,
                name: '"Рога и Копыта" Корпорейшн',
                logo: 'https://avatars.mds.yandex.net/get-connect/1540619/c7c31a20-2597-11ea-b1f5-094a802e30d2/orig',
            },
        ],
    },
    js: {
        live: false,
        mailCallerId: 'lego'
    }
}
```

<a name="mods-fetch-organizations"></a>

#### Модификатор `fetch-organizations`

ajax-загрузка организаций пользователя.

> **Примечание.** Инициализируется через `organizationsDataProvider`.

Допустимые значения: `yes`.

Способ установки: `BEMJSON`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    mods: {
        'fetch-accounts': 'yes',
        'with-organizations': 'yes',
        'fetch-organizations': 'yes',
    },
    uid: 6789054321,
    yu: 123456789012345678,
    retpath: 'https://yandex.ru',
    passportHost: 'https://passport.yandex.ru',
    name: 'Денис Кузнецов',
    js: {
        live: false,
        accountsDataProvider: 'accounts-mock-provider',
        organizationsDataProvider: 'organizations-mock-provider',
        mailCallerId: 'lego'
    }
}
```

<a name="mods-with-pin-code"></a>

#### Модификатор `with-pin-code`

Наличие кнопки генерации Pin-кода.

Допустимые значения: `yes`.

Способ установки: `BEMJSON`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    mods: {
        'with-зшт-сщву': 'yes',
    },
    uid: 6789054321,
    yu: 123456789012345678,
    retpath: 'https://yandex.ru',
    passportHost: 'https://passport.yandex.ru',
    name: 'Денис Кузнецов',
    js: {
        live: false,
        mailCallerId: 'lego'
    }
}
```

#### Поле `uid`

Определяет уникальный идентификатор пользователя.

Тип: `Number`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    yaplus: false,
    uid: 84473936,
    yu: 123456789012345678,
    retpath: 'https://yandex.ru',
    passportHost: 'https://passport.yandex.ru',
    name: 'Денис Кузнецов'
}
```

<a name="field-yu"></a>

#### Поле `yu`

Определяет cookie-файлы `yandexuid`.

Тип: `Number`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    yaplus: false,
    uid: 84473936,
    yu: 123456789012345678,
    retpath: 'https://yandex.ru',
    passportHost: 'https://passport.yandex.ru',
    name: 'Денис Кузнецов'
}
```

<a name="field-yaplus"></a>

#### Поле `yaplus`

Определяет у пользователя наличие подписки Плюс.

В значении:

- `false` — плюс доступен, но не подключен. Отображается ссылка **Получить Плюс**.
- `true` - плюс доступен, подключен. Отображается кнопка  **плюс**.

В случае, если ничего не передано, пункт меню не появляется.

Тип: `Boolean`.

```js
{
    block: 'x-table',
    attrs: { style: 'float: right;' },
    head: ['false', 'true'],
    body: [
        [false, true].map((yaplus) => {
            return {
                block: 'user2',
                yaplus: yaplus,
                uid: 84473936,
                yu: 123456789012345678,
                retpath: 'https://yandex.ru',
                passportHost: 'https://passport.yandex.ru',
                name: 'Денис Кузнецов'
            };
        })
    ]
}
```

<a name="field-hat"></a>

#### Поле `hat`

Определяет объект баннера, встраиваемого в меню блока. Реализуется блоком `user-hat`. Необходимо использовать совместно с модификатором `has-hat`.

Тип: `BEMJSON`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    yaplus: false,
    mods: { 'has-hat': 'yes' },
    hat: {
        block: 'user-hat',
        fetchUrl: 'https://yabs.yandex.ru/page/280743',
        mods: { 'fetch-data': 'yes' }
    },
    uid: 84473936,
    yu: 123456789012345678,
    retpath: 'https://yandex.ru',
    passportHost: 'https://passport.yandex.ru',
    name: 'Денис Кузнецов'
}
```

<a name="field-retpath"></a>

#### Поле `retpath`

Определяет URL страницы. По умолчанию `location.href`.

Тип: `String`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    uid: 84473936,
    yu: 123456789012345678,
    retpath: 'https://yandex.ru',
    passportHost: 'https://passport.yandex.ru',
    name: 'Денис Кузнецов'
}
```

<a name="field-avatarId"></a>

#### Поле `avatarId`

Определяет идентификатор аватарки пользователя.

- Если передан идентификатор, аватарка отобразится.
- Если передано значение `false`, аватарка не выводится.
- При любых других `falsy`-значениях выводится «заглушка».

Тип: `String`.

```js
{
    block: 'x-table',
    attrs: { style: 'float: right;' },
    head: ['false', '20706/84473936-5041676'],
    body: [
        [false, '20706/84473936-5041676'].map((avatar) => {
            return {
                block: 'user2',
                avatarId: avatar,
                uid: 6789054321,
                yu: 123456789012345678,
                retpath: 'https://yandex.ru',
                passportHost: 'https://passport.yandex.ru',
                name: 'Иван Персидский'
            };
        })
    ]
}
```

<a name="field-origin"></a>

#### Поле `origin`

Определяет название текущего сервиса с `user2`.

Тип: `String`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    uid: 84473936,
    yu: 123456789012345678,
    retpath: 'https://yandex.ru',
    passportHost: 'https://passport.yandex.ru',
    name: 'Денис Кузнецов',
    origin: 'Яндекс.Дзен'
}
```

<a name="field-camera"></a>

#### Поле `camera`

Определяет наличие иконки фотоаппарата на стандартном аватаре в шапке выпадающего меню.

Тип: `Boolean`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    uid: 84473936,
    yu: 123456789012345678,
    retpath: 'https://yandex.ru',
    passportHost: 'https://passport.yandex.ru',
    name: 'Денис Кузнецов',
    camera: true
}
```

<a name="field-name"></a>

#### Поле `name`

Определяет имя пользователя.

- Если передано `false`, имя пользователя не выводится.
- При любых других `falsy`-значениях выводится `uid` пользователя.

Тип: `String`.

```js
{
    block: 'x-table',
    attrs: { style: 'float: right;' },
    head: ['false', 'Денис Кузнецов'],
    body: [
        [false, 'Денис Кузнецов'].map((name) => {
            return {
                block: 'user2',
                uid: 84473936,
                name: name
            };
        })
    ]
}

```

<a name="field-maxLength"></a>

#### Поле `maxLength`

Определяет максимально видимую длину имени пользователя. По умолчанию количество видимых символов `16`.

Тип: `Number`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    uid: 6789054321,
    yu: 123456789012345678,
    name: 'Денис Кузнецов',
    maxLength: 10
}
```

<a name="field-unreadCount"></a>

#### Поле `unreadCount`

Определяет количество видимых непрочитанных писем.

Тип: `Number`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    uid: 6789054321,
    yu: 123456789012345678,
    unreadCount: 7,
    name: 'Денис Кузнецов'
}
```

<a name="field-passportHost"></a>

#### Поле `passportHost`

Определяет URL страницы паспорта. По умолчанию берётся из `i-services` – `.serviceUrl('passport')`.

Тип: `String`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    uid: 6789054321,
    yu: 123456789012345678,
    passportHost: 'https://passport.yandex.ru',
    name: 'Денис Кузнецов'
}
```

#### Поле `source`

Идентификатор сервиса. Это то, что сервис, встраивающий блок, может передать, чтобы себя идентифицировать.

Тип: `String`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    uid: 6789054321,
    yu: 123456789012345678,
    source: 'connect',
    name: 'Денис Кузнецов'
}
```


#### Поле `preset`

Предопределённый набор сервисов, используемых в организациях Коннекта.

Тип: `String`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    uid: 6789054321,
    yu: 123456789012345678,
    preset: '[]',
    name: 'Денис Кузнецов'
}
```


#### Поле `secretKey`

Секретный ключ.

Тип: `String`.

```js
{
    block: 'user2',
    attrs: { style: 'float: right;' },
    uid: 6789054321,
    yu: 123456789012345678,
    secretKey: 'sc',
    name: 'Денис Кузнецов'
}
```
