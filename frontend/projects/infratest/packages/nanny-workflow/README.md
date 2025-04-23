# Nanny Workflow

Инструменты для работы с Nanny.

## Установка

```console
npm i @yandex-int/trendbox-ci.nanny-workflow --registry=https://npm.yandex-team.ru
```

## API

### createRelease

Создаёт релиз в Nanny из локальной директории (файла) или готового ресурса в Sandbox.

#### Пример

```js
const { createRelease, DUPLICATE_POLICY_TYPES, RELEASE_TYPES } = require('@yandex-int/trendbox-ci.nanny-workflow');

await createRelease({
    resourcePath: './build'
    resourceType: 'REPORT_TEMPLATES_PACKAGES',
    title: 'report-templates/r1774/serp/chat@v0.31.1 (hotfix)',
    description: ```
        Релиз chat
        https://st.yandex-team.ru/SEAREL-5117

        Список изменений:

        MSSNGRFRONT-64 - При обновлении страницы пропадает открытый чат
    ```.trim(),
    emailNotifyTo: ['sanity@yandex-team.ru', 'coffeeich@yandex-team.ru'],
    emailNotifyCc: ['infraduty@yandex-team.ru'],
    releaseType: RELEASE_TYPES.TESTING,
    duplicatePolicyType: DUPLICATE_POLICY_TYPES.IGNORE
});
```

В Nanny релиз выглядит следующим образом.

![nanny-release](./assets/nanny-release.png)

#### Как это работает?

Nanny работает с понятием «[релиза в Sandbox](sandox-release)» — это Sandbox-задача и её дочерние ресурсы, которые перешли в определённый статус.

Под капотом происходит следующее:

1. Cоздаётся ресурс указанного типа с указанной директорией (файлом) (этот шаг будет пропущен если указан `resourceId` в параметрах).
1. Cоздаётся специальная Sandbox-задача, которая принимает на вход полученный ресурс.
1. Ресурс скачивается и становится дочерним по отношению к Sandbox-задаче `(2)`.
1. Sandbox-задача `(2)` релизится в указанный статус.
1. Отправляется запрос на создание релиза в Nanny.

> [Подробнее](sandbox-and-nanny-integration) о том, что происходит, когда Nanny узнаёт о релизе от Sandbox.

#### Переменные окружения

##### NANNY_TOKEN

В переменной окружения `NANNY_TOKEN` должен быть указан токен пользователя от имени которого будет создан релиз в Nanny. Узнать свой токен можно на [странице oauth](nanny-oauth) в Nanny.

#### Опции

#### nannyServiceId *

Идентификатор сервиса в Nanny. Скрипт будет дожидаться переключения активной конфигурации в указанном сервисе.

#### resourcePath *

Путь к локальной папке или файлу.

> Подробнее на [wiki](sandbox-wiki)

#### resourceType *

Тип ресурса в Sandbox. Важно, чтобы пользователь от имени которого будет релизиться ресурс находился в `releasers` указанного типа ресурса. [Подробнее про релизы](sandbox-release-rights) в Sandbox.

#### sandboxOwner *

Группа в Sandbox в которой будет запускаться таска `NANNY_RELEASE_RESOURCE`.

> :warning: автор таски (под чьим токеном запускается скрипт) должен быть указан в соответствующей группе в Sandbox.

#### resourceId *

Если хочется зарелизить уже существующий ресурс в Sandbox — можно указать его идентификатор.

> :warning: В таком случае опции `resourcePath` и `resourceType` становятся необязательными и игнорируются.

#### sandboxToken *

Токен пользователя от имени которого будет релизиться ресурс в Sandbox. Узнать свой токен можно на [странице oauth](sandbox-oauth) в Sandbox.

##### baseSandboxURL

Базовый урл Sandbox. По умолчанию, продакшен (`https://sandbox.yandex-team.ru`).

##### title

Название релиза.

##### emailNotifyTo

Настройки уведомлений на почту о выкатке релиза. На эти адреса будут отправлены письма о выкатке релиза.

##### emailNotifyCc

Настройки уведомлений на почту о выкатке релиза. Эти адреса будут включены в копию письма о выкатке релиза.

##### startrekTicketIds

Список тикетов в Tracker в которые робот `nanny-robot` оставит комментарии о состоянии релиза. [Подробнее](nanny-ticket-comments).

> :warning: Чтобы Nanny могла отправлять комментарии необходимо выдать права роботу `nanny-robot` в соответствующей очереди.

##### webhookUrls

Список URL'ов куда Nanny сделает POST-запрос после закрытия релиза (перехода в статус `CLOSED`).

> [Пример](nanny-webhook-body-example) тела запроса.

Вебхуки также сработают, если в закрытом релизе один из тикетов перейдет в статус `DEPLOY_SUCCESS` или из статуса `DEPLOY_SUCCESS` в любой другой.

##### releaseType

Тип релиза в Sandbox, например, `testing`, `prestable` или `stable`.

> Подробнее в [АПИ Sandbox](sandbox-api).

##### duplicatePolicyType

Политика обработки дубликатов релиза.

Возможные значения (`enum`):

* `CLOSE_AS_DUPLICATE`
* `IGNORE` (по умолчанию)

> [Подробнее](nanny-duplication-policy) про логику закрытия дублей в Nanny.

##### component

Компонент релиза. Используется для поиска дубликатов. По умолчанию, пустая строка.

##### nannyTags

Метки, которые будут добавлены к релизу (для фильтрации в Nanny).

##### sandboxTags

Теги для фильтрации релизных тасок в Sandbox.

##### ensureDeploy

Если true, то программа будет дожидаться деплоя релиза.

Программа будет опрашивать состояние релиза и связанных тикетов в Nanny. Если какой-то тикет перейдёт в один из статусов (`CANCELLED`, `DEPLOY_FAILED`, `ROLLED_BACK`) или выйдет время ожидания деплоя, то такой релиз будет неуспешным и программа упадёт с ошибкой.

##### ensureDeployInterval

Количество секунд между итерациями проверки статуса деплоя. По умолчанию 180 секунд.

##### ensureDeployAttempts

Количество попыток проверить статус деплоя. По умолчанию 10.

[sandbox-release]: https://wiki.yandex-team.ru/sandbox/releases/
[sandbox-release-rights]: https://wiki.yandex-team.ru/sandbox/releases/#prava
[sandbox-and-nanny-integration]: https://nda.ya.ru/3UW9E8
[sandbox-wiki]: https://nda.ya.ru/3UW9E9
[sandbox-oauth]: https://sandbox.yandex-team.ru/oauth
[nanny-oauth]: https://nanny.yandex-team.ru/ui/#/oauth/
[nanny-ticket-comments]: https://nda.ya.ru/3UW9Dz
[nanny-webhook-body-example]: https://nda.ya.ru/3UW9E7
[sandbox-api]: https://nda.ya.ru/3UW8sN
[nanny-duplication-policy]: https://nda.ya.ru/3UVnKk
