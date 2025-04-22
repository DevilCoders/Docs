# Автотесты в КВ

-   [Hermione-тесты](#Hermione-тесты)
    -   [Создание страницы](#Создание-страницы)
    -   [Хелпер userStory](#Хелпер-userStory)
    -   [Хелперы permissions](#Хелперы-permissions)

## Hermione-тесты

Базовую инструкцию читайте на [вики](https://wiki.yandex-team.ru/market/verstka/vendors/autotests/).

### Создание страницы

Базовым сьютом является страница (она же точка входа для каждого теста).
Она располагается в `spec/hermione/test-suites/pages`. Каждая страница соответствует реальному разделу Кабинета.
Внутри неё на каждого пользователя создается отдельная [userStory](#Хелпер-userStory) для тестирования ролевой модели.

Если раздел новый, или всё ещё не покрыт АТ, то нужно завести страничный сьют следующим образом:

1. в `spec/hermione/test-suites/pages` создать новую директорию с названием в camelCase-нотации
   (старайтесь, чтобы название соответствовало названию раздела из `src/pages`, например, `UserProfile`);
2. внутри директории создать файл с названием в kebab-нотации, например, `user-profile.hermione.js`
   (важно, чтобы формат соответствовал `*.hermione.js`, иначе он не подхватится при сборке тест-пака);
3. написать базовую реализацию страничного сьюта:

```js
'use strict';

const makeUserStory = require('helpers/userStory');
const USERS = require('spec/lib/constants/users/users');
const {mergeSuites, makeSuite} = require('ginny');

const ROUTE_NAMES = require('app/constants/routeNames');

const userStory = makeUserStory(ROUTE_NAMES.USER_PROFILE); // TODO (1): Укажите адрес страницы из ROUTE_NAMES

module.exports = makeSuite('Страница Профиля пользователя', {
    // TODO (2): Задайте название в формате "Страница [Название]"
    story: (() => {
        const suites = USERS.map(user => {
            const {description} = user;

            return makeSuite(description, {
                story: userStory({
                    user,
                    pageObjects: {
                        logo: 'Logo',
                        footer: 'Footer',
                    },
                    suites: {
                        common: [
                            {
                                suite: 'Page/title',
                                params: {
                                    title: 'Профиль пользователя', // TODO (3): Укажите document.title
                                },
                            },
                        ],
                    },
                }),
            });
        });

        return mergeSuites(...suites);
    })(),
});
```

### Хелпер userStory

Предназначен для оптимизации написания страничных сьютов.

#### Предназначение

-   установка моков для [кадаврика](https://github.yandex-team.ru/market/kadavrique)
-   открытие тестируемой страницы и авторизация в тестовом Паспорте
-   проверка доступности страницы
-   упрощенная сборка страничных сьютов, если страница доступна

А также:

-   добавление теста на логотип
-   скрытие информеров типа "дятел" на время теста

#### Параметры

-   `{boolean} skipAuth`\
    **Default:** `false`\
    Пропускает переход на URL-страницы.

-   `{boolean} checkPageAvailability`\
    **Default:** `true`\
    Добавляет тесты на доступность страницы.

-   `{Object} user`\
    Данные пользователя.

-   `{Object} suites`\
    Набор страничных сьютов.

    -   `{string|object|Array.<string|object>} suites.common`\
        Сьюты без привязки к пермишенам.
    -   `{[key: string]: string|object|Array.<string|object>} suites.byPermissions`\
        Коллекция сьютов с привязкой к пермишенам.

-   `{Object} params`\
    Глобальные параметры сьютов.

    -   `{number} params.vendor`\
        Идентификатор вендора.

    -   `{Object} params.routeParams`\
        Query-параметры URL-адреса страницы.

-   `{[key: string]: string|Function} pageObjects`\
    Коллекция глобальных PO.

-   `{Function} onSetKadavrState`\
    Коллбек установки моков кадаврика.

-   `{Function} beforeEach`\
    Коллбек начала выполнения теста.

-   `{Function} afterEach`\
    Коллбек завершения выполнения теста.

#### Пример вызова

```js
const {userStory} = require('helpers/userStory')('pageRouteName');

userStory({
    user,
    params: {
        vendor: 3301,
        routeParams: {
            vendor: 3301,
        },
    },
    onSetKadavrState({id}) {
        switch (id) {
            // Установка стейта для отдельного тест-кейса по ID
            case 'vendor_auto-XXX':
                return this.browser.setState('userProfileState', {
                    name: 'Аркадий',
                    avatarSrc: 'picture.jpg',
                });

            default:
                return this.browser.setState('vendorsState', initialState);
        }
    },
    pageObjects: {
        logo: 'Logo',
        footer() {
            return this.createPageObject('Footer');
        },
    },
    suites: {
        common: [
            'UserProfile',
            {
                suite: 'Page/title',
                params: {
                    title: 'Профиль пользователя',
                },
            },
        ],
        byPermissions: {
            [PERMISSIONS.userProfile.read]: 'UserProfile/viewing',
            [PERMISSIONS.userProfile.write]: {
                suite: 'UserProfile/editing',
                meta: {
                    id: 'vendor_auto-XXX',
                },
            },
        },
    },
});
```

### Хелперы permissions

Предназначены для указания в ключах коллекции byPermissions внутри [userStory](#Хелпер-userStory) комбинации пермишенов.

#### combinePermissions

Объединяет пермишены (логическое "или"). Тест добавляется в тест-пак при наличии у пользователя **хотя бы одного** пермишена из списка.

```js
const {combinePermissions} = require('helpers/permissions');

byPermissions: {
    [combinePermissions(
        PERMISSIONS.entries.read,
        PERMISSIONS.entries.write,
    )]: 'SuiteName',
}
```

#### excludePermissions

Исключает пермишены. Тест добавляется в тест-пак при отсутствии у пользователя **всех** пермишенов из списка.

```js
const {excludePermissions} = require('helpers/permissions');

byPermissions: {
    [excludePermissions(
        PERMISSIONS.entries.read,
        PERMISSIONS.entries.write,
    )]: 'SuiteName',
}
```

#### allPermissions

Пересекает пермишены (логическое "и"). Тест добавляется в тест-пак при наличии у пользователя **всех** пермишенов из списка.

```js
const {allPermissions} = require('helpers/permissions');

byPermissions: {
    [allPermissions(
        PERMISSIONS.offerta.write,
        PERMISSIONS.recommended.write,
    )]: 'SuiteName',
}
```

#### Комбинация combinePermissions и excludePermissions

Тест добавляется в тест-пак при выполнении условий:

-   у пользователя присутствует **хотя бы один** пермишен из аргументов combinePermissions
-   у пользователя отсутствуют **все** пермишены из аргументов excludePermissions

Например, добавление теста **только** для читающего менеджера:

```js
const {combinePermissions, excludePermissions} = require('helpers/permissions');

byPermissions: {
    [combinePermissions(
        PERMISSIONS.entries.read,
        excludePermissions(PERMISSIONS.entries.write),
    )]: 'SuiteName',
}
```

ВНИМАНИЕ! При обратной вложенности результат будет отличаться. Справедливо и для allPermissions.

```js
const {combinePermissions, excludePermissions} = require('helpers/permissions');

byPermissions: {
    [excludePermissions(
        PERMISSIONS.entries.read,
        combinePermissions(PERMISSIONS.entries.write),
    )]: 'SuiteName',
}
```

Эквивалентно одиночному excludePermissions:

```js
const {combinePermissions, excludePermissions} = require('helpers/permissions');

byPermissions: {
    [excludePermissions(
        PERMISSIONS.entries.read,
        PERMISSIONS.entries.write,
    )]: 'SuiteName',
}
```
