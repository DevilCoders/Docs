# i18n-ts

[![npm version](https://badger.yandex-team.ru/npm/@yandex-data-ui/i18n-ts/version.svg)](https://npm.yandex-team.ru/@yandex-data-ui/i18n-ts)
[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=travel/frontend/i18n-ts&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/i18n-ts)
[![oko vulnerabilities](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=travel/frontend/i18n-ts&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/i18n-ts)
[![distribution health](https://badger.yandex-team.ru/oko/pkg/@yandex-data-ui/i18n-ts/health.svg)](https://oko.yandex-team.ru/pkg/@yandex-data-ui/i18n-ts)

Пакет для сборки переводов в TS модули.

## Installation

```
npm install --save-dev @yandex-data-ui/i18n-ts
```

## Usage example

1. Скачайте и соберите переводы, [примеры сборки](./example/README.md).

2. Для удобства добавьте алиас `i18n` в вашу систему сборки, на папку с собранными переводами.

3. Настройте сборку проекта для каждого языка вашего проекта, в каждой сборке укажите глобальную константу `__BUILD_LANG__`, для webpack, например через [DefinePlugin](https://webpack.js.org/plugins/define-plugin/).

4. Используйте перевод в коде

```tsx
import React from 'react';
import * as i18n from 'i18n/SomeComponent';

const SomeComponent: React.FC = () => {
    return <div>{i18n.someTextKey({paramKey: 'value'})}</div>;
};

export default SomeComponent;
```

, где `SomeComponent` - имя кейсета, `someTextKey` - имя ключа, `paramKey` - имя параметра

Другие продвинутые примеры использования смотрите в [примерах](docs/examples.md).

## Motivation

Пакет решает следующие проблемы при доставке переводов в код:

1. Поддержка шаблонов: вставка переменных или верстки, plural, if.
2. Проверка наличия кейсетов и ключей на этапе сборки
3. Возможность размещать ключи (или кейсеты) по разным бандлам по мере использования, а
   неиспользуемые ключи в бандл не должны попадать.
4. Компиляция шаблонов из танкера во время сборки с проверкой на ошибки (тайпчек).
5. Обработка на этапе компиляции шаблонов, вставка неразрывных пробелов,
   удаление лишних пробелов и тд
6. Вставка в шаблоны React компонентов

А также некоторые другие [проблемы](docs/advantages.md).

## Template

Переводы поддерживают следующие возможности шаблонизации.

### Вставка переменной

Перевод keySet: `account`, key: `welcomeUser`

```
Добро пожаловать, {{userName}}
```

Использование:

```ts
import * as i18n from 'i18n/account';

// Добро пожаловать, Ivan
i18n.welcomeUser({userName: 'Ivan'});
```

### Условие

#### if/else

Перевод keySet: `account`, key: `welcomeUser`

```
{{#if hasUserName}}А мы вас знаем{{else}}Представьтесь, пожалуйста{{/if}}
```

Использование:

```ts
import * as i18n from 'i18n/account';

// А мы вас знаем
i18n.welcomeUser({hasUserName: true});

// Представьтесь, пожалуйста
i18n.welcomeUser({hasUserName: false});
```

#### Только if

Перевод keySet: `tickets`, key: `warning`

```
{{#if hasAlarm}}ВНИМАНИЕ!{{/if}} Билеты в кассах
```

Использование:

```ts
import * as i18n from 'i18n/tickets';

// ВНИМАНИЕ! Билеты в кассах
i18n.warning({hasAlarm: true});

// Билеты в кассах
i18n.warning({hasAlarm: false});
```

#### if/else с параметрами

Перевод keySet: `warnings`, key: `manyPeople`

```
{{#if peopleCount > 5}}А вас много{{else}}Вас мало{{/if}}
```

Использование:

```ts
import * as i18n from 'i18n/warnings';

// Вас мало
i18n.manyPeople({peopleCount: 1});

// А вас много
i18n.manyPeople({peopleCount: 6});
```

### Числительные

Перевод keySet: `comments`, key: `reviewsCount`

```
{{reviewsCount}} {{plural count=reviewsCount one="отзыв" some="отзыва" many="отзывов"}}
```

one - форма числительного для 1, 21, 31 ...
some - форма для 2, 3, 4 ...
many - форма для 5, 6, 7 ...

Использование:

```ts
import * as i18n from 'i18n/warnings';

// 1 отзыв
i18n.reviewsCount({reviewsCount: 1});

// 2 отзыва
i18n.reviewsCount({reviewsCount: 2});

// 6 отзывов
i18n.reviewsCount({reviewsCount: 6});
```

## Migration

[Пример миграции](migration/README.md) с ymaps-tanker с помощью js-codeshift.

### Функция i18n

Для более плавного переезда можно собрать функцию с интерфейсом как из ymaps-tanker `i18n(keySetName: string, keyName: string, params?: object)`.
Для этого в `Builder` надо передать параметр `i18nBackwardCompatibility: true`,
и опционально можно указать имя файла с функцией в параметре: `i18nBackwardCompatibilityFileName`, по умолчанию - `index`.

Для использования этого метода нужно создать функцию обертку, которая:

1. Умеет обрабатывать исключения: нет кейсета или ключа.
2. Трансформирует имя ключа в имя функции по вашим правилам.

Например:

```ts
import getFunctionName from '@yandex-data-ui/i18n-ts/client/getFunctionName';

import i18nOriginal from 'i18n';

const i18n: typeof i18nBuild = (keySetName, keyName, params) => {
    try {
        return i18nOriginal(keySetName, getFunctionName(keyName), params);
    } catch (e) {
        // Здесь можно залогировать ошибку

        return '';
    }
};

export default i18n;
```

#### Disclaimer

Так как этот файл импортирует все кейсеты, то для него недоступен тайпчек и code-splitting.
Использовать эту функцию нужно только на время переезда для обратной совместимости.

## KeyName

Предложенный подход накладывает ограничение на имена ключей, так как после сборки они станут именами функций.
То есть теперь имена ключей не должны:

1. Содержать `.`, `-`.
2. Быть ключевыми словами языка `case`, `switch`, `function` ... .

Поэтому во время сборки имена по умолчанию трансформируются с помощью
`import getFunctionName from '@yandex-data-ui/i18n-ts/client/getFunctionName';`.
Но это поведение можно изменить, передав свою функцию преобразование ключа к имени функции
`(key: string) => string` в конструктор Builder в параметре `prepareKey`.
Если вы используете метод `unsafeDynamicKeyset`, то нужно передать свою функцию в параметр `prepareKey` тоже.

Рекомендуется использовать camelCase для названий ключей, чтобы ключи не трансформировались в результате сборки.

## Новый Танкер

Для переезда на новый танкер потребуется:

1. Скачивать ключи через новое API, для этого нужно передать новый `baseUrl` до нового API Танкера в конструктор `TankerDownloader`.
   Например:

```ts
const downloader = new TankerDownloader({
    baseUrl: 'http://tanker-api.test.yandex-team.ru/',
    //...
});
```

_Примечание: на момент написания документации тестовое апи нового танкера использует self-signed сертификат,
чтобы игнорировать эту проверку можно использовать переменную окружения `NODE_TLS_REJECT_UNAUTHORIZED=0`_

2. Изменить формирование ссылок. Так как в новом Танкере меняется вид ссылки до кейсетов и ключей.

Было: **UI_BASE**/?project=**PROJECT**&branch=**BRANCH**&keyset=**KEYSET**&key=**KEY**

Стало: **UI_BASE**/project/**PROJECT**/keyset/**KEYSET**/key/**KEY**?branch=**BRANCH**

Чтобы корректно сформировать ссылки в новый танкер
нужно передать новый UI Танкера `tankerLinkOptions.base`
и включить новый формат `tankerLinkOptions.isNewTanker`
через параметры в конструкторе `Builder`.
Например:

```ts
const builder = new Builder({
    tankerLinkOptions: {
        base: 'http://sandbox.tanker-beta.yandex-team.ru',
        isNewTanker: true,
        // ...
    },
    // ...
});
```

## Support

Присылайте Issues, PRs или пишите [@isaven](https://staff.yandex-team.ru/isaven).
