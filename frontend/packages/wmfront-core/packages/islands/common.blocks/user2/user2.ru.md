## Описание
`user2` – блок пользователя, расположенный в правой части шапки страницы.

### Элементы блока
Блок неавторизованного пользователя состоит из кнопки «Войти», для авторизации на Яндексе.
Отображается, если не был передан идентификатор пользователя (параметр `uid`). Надпись на кнопке и текст всплывающей подсказки локализуются автоматически. В отличие от блока `user`, эта кнопка перенаправляет на Паспорт, а не открывает `domik`.
На `touch-phone`-уровне вместо кнопки с текстом и иконкой выводится только кнопка с иконкой входа.

Блок пользователя, авторизованного любым доступным способом (логин/пароль, [социальная авторизация](https://wiki.yandex-team.ru/passport/social/about)), может состоять из следующих **основных элементов**:
* [имени и иконки пользователя (__current-account)](#uaccount);
* [выпадающего меню пользователя (__popup)](#upopup);

<a name="uaccount"></a>
#### `__current-account`: аккаунт пользователя
Текущий аккаунт пользователя.
По умолчанию (если параметры `avatarId` и `name` не `false`) выводятся аватар со счётчиком непрочитанных писем и имя с акцентированной красной буквой.
В коде элемента формируется BEMJSON блока [user-account](../user-account/user-account.ru.md) с учётом переопределяемых значений в параметре `userAccount`. Например:

```javascript
{
    block: 'user2',
    uid: 123123123,
    yu: 123456789012345678,
    retpath: 'https://yandex.ru',
    passportHost: 'https://passport.yandex.ru',
    userAccount: {
        mods: {
            'has-accent-letter': false,
            'hide-name': 'yes'
        },
        avatarHost: 'https://avatars.mds.yandex.net'
    }
}
```
По переданным параметрам для `user-account` будет сформирован BEMJSON:

```javascript
{
    block: 'user-account',
    mix: {block: 'user2', elem: 'current-account', elemMods: this.elemMods},
    mods: {
        'has-ticker': false,
        'has-accent-letter': false,
        'hide-name': 'yes'
    },
    name: '123123123', // uid
    url: 'https://passport.yandex.ru',
    pic: {avatarId: undefined}, // будет выведена «заглушка»
    avatarHost: 'https://avatars.mds.yandex.net'
}
```

<a name="upopup"></a>
#### `__popup`: выпадающее меню пользователя
Внутри `__popup` выводится элемент `__menu` со следующей структурой по умолчанию:
* Группа меню
    * Количество непрочитанных писем (`mail`);
    * Написать письмо (`mail-compose`),
    * Загрузить файл (`disk`);
* Группа меню
    * Настройки (`settings`);
    * Паспорт (`passport`);
* Группа аккаунтов пользователя
    * Аккаунты
    * Добавить аккаунт
* Группа меню мультиавторизации
    * Редактировать список (`edit-accounts`);
    * Выход (`exit`)

#### Другие элементы блока
* `__menu` – основной элемент меню. Внутри используется блок `menu`. В контенте выводятся сгруппированные `__menu-item` и элемент `__multi-auth`;
* `__multi-auth` – мультиавторизация. Состоит из списка аккаунтов пользователя и меню мультиавторизации;
* `__accounts` – аккаунты пользователя. Состоит из списка аккаунтов и ссылки «Добавить пользователя». Принимает параметры `{addAccount: {}, accounts: []}`;
* `__add-account` – выводит блок `user-account` с предустановленными значениями полей `{name: 'Добавить пользователя'}` и `{url: passportHost + '/auth?mode=add-user}`;
* `__enter` – кнопка с иконкой и текстом «Войти». Отображается для неавторизованного пользователя;
* `__accounts-provider` – провайдер данных об аккаунтах пользователя. Расширяет блок `i-request_type_ajax`;
* `__unread-provider` – провайдер данных об аккаунтах пользователя. Расширяет блок `i-request_type_ajax`;

### Параметры блока:
##### Основные параметры
* `uid` – идентификатор пользователя;
* `yu` – куки `yandexuid`;
* `retpath` – URL страницы, по умолчанию берётся `location.href`;
* `avatarId` – идентификатор аватарки пользователя. Если передано `false`, аватарка не выводится. При любых других `falsy`-значениях выводится «заглушка»;
* `name` – имя пользователя. Если передано `false`, имя пользователя не выводится. При любых других `falsy`-значениях выводится `uid` пользователя;
* `unreadCount` – количество непрочитанных писем;
* `passportHost` – URL Паспорта. По умолчанию берётся из `i-services` – `.serviceUrl('passport')`;
* `accountsUrl` – **JS-параметр** – URL сервиса аккаунтов в Паспорте. По умолчанию берётся из `i-services` – `.serviceUrl('pass') + /accounts`;
* `exportHost` – **JS-параметр** – URL сервиса для запроса количества непрочитанных писем. По умолчанию `https://export.yandex.ru`;
* `accountsDataProvider` – **JS-параметр** провайдер данных об аккаунтах пользователя от сервера. Значение по умолчанию: `user2__accounts-provider`;
* `accountsMax` – **JS-параметр** максимальное количество отображаемых в меню аккаунтов пользователя. По умолчанию 5;
* `unreadDataProvider` – **JS-параметр** провайдер данных о непрочитанных письмах. По умолчанию `user2__unread-provider`;
* `mailCallerId` – **JS-параметр** идентификатор потребителя. Подробнее о том, как [получить идентификатор](https://wiki.yandex-team.ru/users/jkennedy/api2/).

##### Параметры аккаунта
* `userAccount` – переопределяемые параметры для блока `user-account`. Используется, если контент блока `user2` не передан или передан элемент `__current-account`;

##### Параметры выпадающего меню
* `accounts` – BEMJSON массив аккаунтов пользователя (блоки `user-account`).
* `addAccount` – пользовательская ссылка «Добавить пользователя». По умолчанию выводится иконка символа «+» и текст «Добавить пользователя». Текст можно переопределить, передав здесь `{name: 'Custom text'}`;
* `actionsMenu` – пользовательское меню. Принимается массив объектов, где каждый объект рассматривается как группа меню:
```javascript
{
    actionsMenu: [
        {
            items: [
                {action: 'mail'},
                {action: 'mail-compose'}
            ]
        },
        {
            items: [
                {action: 'settings'}
            ]
        }
    ]
}
```
* `multiAuthMenu` – пользовательское меню мультиавторизации. Принцип работы такой же, как у `actionsMenu`.

### Модификаторы блока
* `_fetch-accounts` – в значении `yes` расширяет js-реализацию блока. При инициализации блока через `accountsDataProvider` получает и отображает в `__multi-auth` аккаунты пользователя;
* `_fetch-unread` – в значении `yes` расширяет js-реализацию блока. При инициализации блока через `unreadDataProvider` получает и отображает количество непрочитанных писем;
* `_fetch-counters` – в значении `yes` расширяет js-реализацию блока. Получает и отображает количество непрочитанных писем **для всех аккаунтов пользователя**. Чтобы получить список непрочитанных писем сразу и при этом не обращаться к ручке дважды, можно отключить ленивую инициализацию блока.
Предоставляет публичный метод `updateCounters`. Метод принимает параметр `force` булевого типа, в значении `true` параметр форсирует отправление нового запроса.
В отличие от `_fetch-unread` забирает аккаунты из новой ручки, для использования которой необходимо передать идентификатор потребителя в качестве `JS`-параметра `mailCallerId`. Подробнее о том, как [получить идентификатор](https://wiki.yandex-team.ru/users/jkennedy/api2/);
* `_has-logout` – в значении `yes` добавляет аккаунтам авторизованных пользователей в меню мультиавторизации элемент `__logout`. При клике по элементу `__logout` блок `user2` вызывает событие `logout-click`.

Пример:

```javascript
{
    block: 'user2',
    mods: {
        'fetch-accounts': 'yes',
        'fetch-unread': 'yes'
    },
    uid: 84473936,
    yu: 123456789012345678,
    retpath: 'https://yandex.ru',
    passportHost: 'https://passport.yandex.ru',
    name: 'John Doe',
}
```

Пример использования модификатора `_fetch-counters`:

```javascript
{
    block: 'user2',
    mods: {
        'fetch-accounts': 'yes',
        'fetch-counters': 'yes'
    },
    js: {
        mailCallerId: 'morda'
    }
    ...
}
```
