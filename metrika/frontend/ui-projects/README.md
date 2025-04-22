# Metrika Frontend Monorepo

## Тестирование

Тесты можно запустить следующими командами:

-   все тесты `npm test`
-   серверные тесты `npm test server`
-   клиентские тесты `npm test client`
-   тесты библиотеки компонентов (mindstorms) `npm test mindstorms`

## Тестирование скриншотами

Пример теста для
[Button](https://a.yandex-team.ru/arc_vcs/metrika/frontend/ui-projects/client/src/libs/mindstorms/components/button/__test/button.test.tsx)

### Как добавить

Внутри папки компонента создать директорию `test` и добавить в неё файл в формате `Component.test.tsx`

Затем импортировать компонент с моковыми данными из сторибука и описать тест с `makeScreenshot`:

```
import { makeScreenshot } from '@client-utils/jest/makeScreenshot';

import { Component } from '../Component.stories';

describe('Component', () => {
    it('screenshooter', async () => {
        await makeScreenshot(<Component />);
    });
});
```

Запустить тест:

```
npm test Component
```

### Как обновить

Когда какой-то из снапшотов падает, переходим в `Component/test/__image_snapshots__/__diff_output__` и смотрим различия.
Затем, либо чиним верстку, чтобы тест проходил, либо обновляем скриншоты. Обновление происходит так же как и для
[обычных снапшотов](https://jestjs.io/ru/docs/snapshot-testing) — через флаг `-u`:

```
npm test Component -- -u
```

### Как работает

На отдельном [stage](https://deploy.yandex-team.ru/stages/metrika-frontend-screenshooter) запущен
[сервис](https://github.yandex-team.ru/telephony/ui/tree/develop/services/screenshot-infra), который принимает разметку,
делает скриншот и возвращает картинку

Затем в коде две вспомогательные функции через этот сервис и
[jest-image-snapshot](https://github.com/americanexpress/jest-image-snapshot) делают скриншоты:

-   [toMatchScreenshot](https://a.yandex-team.ru/arc_vcs/metrika/frontend/ui-projects/jest.setup.ts) — смотрит изменился
    ли снапшот компонента и при наличие изменений отправляет верстку в сервис скриншутера, получает картинку и
    сравнивает результат через `toMatchImageSnapshot` из
    [jest-image-snapshot](https://github.com/americanexpress/jest-image-snapshot)
-   [makeScreenshot](https://a.yandex-team.ru/arc_vcs/metrika/frontend/ui-projects/client/src/libs/test-utils/screenshot.ts)
    — через `renderToStaticMarkup` формирует верстку для компонента, подтягивает стили. После чего делает снапшот и
    вызывает [toMatchScreenshot](https://a.yandex-team.ru/arc_vcs/metrika/frontend/ui-projects/jest.setup.ts)

## Глобальные CSS стили

В библиотеке [styles](https://github.yandex-team.ru/Metrika/frontend/v2/client/src/libs/styles) лежат глобальные css
стили и переменные. Для того, чтобы их подключить, необходимо импортировать styles/index.ts в точку входа проекта

## TODO по сборке:

-   DEV server (+)
-   Support css (+)
-   Migrate to TS config in webpack (+)
-   Support DEV / PROD webpack config
-   Jest and test scripts
-   Support images / svg / fonts
-   Check babel plugins
-   Append eslint plugins for browser env
-   Check webpack plugin
-   Final check TS config
-   Build and CI scripts
-   Optimizations
-   Loadable chunks
-   Check package.json fields (support browsers, etc.)
-   i18n
-   Dockerfile and CD scripts
-   Check typescript errors
-   move redux saga to client

## TODO по прототипу

-   Config and build scripts
-   Redux toolkit & entity cache +
-   Saga +
-   Entity storage and selector API +
-   React router & parsing page params
-   Support entity list & pagination

## TODO

-   Research keep alive

## Быстрый старт

Используем и (если надо) устанавливаем актуальную версию Node.js:

```bash
nvm use
```

Устанавливаем зависимости:

```bash
npm run bootstrap
```

1. Добавляем в рут директорию конкретного нодового сервиса (папка server/src/services/<разрабатываемый сервис>/)
   env.development.yml

```yml
apiConfig:
    url: http://mobmetd-testing.metrika.yandex.net
    tvmId: 2000335

authConfig:
    shouldUseBlackboxAuth: false
    fakeUid: <blackbox uid>
    fakeLogin: <login>
    oauthToken: <token>
    csrf:
        isEnabled: false

httpListenPort: 8090

pageTemplateSource:
    localPath: ./client/build/appmetrica-ui/html-resources/

ssrPageSource:
    localPath: ./client/build/appmetrica-ui/index.html

devStaticDirectoryPath: ./client/build/appmetrica-ui/
```

2. Если нет oauth токена с админскими правами, то в idm запрашиваем админскую роль в Аппметрике / Метрике
3. переходим https://oauth.yandex.ru/client/new
    - заполняем название (удобный идентификатор понятный вам),
    - ставим галочку Веб-сервисы
    - вводим в поле CallbackURI — https://oauth.yandex.ru/verification_code
    - ставим галочки с доступами к Appmetrika и Яндекс.Метрика
    - нажимаем кнопку создать
4. Выбираем созданное приложение в списке доступном по адресу https://oauth.yandex.ru/
5. Копируем поле ID и переходим по ссылке https://oauth.yandex.ru/authorize?response_type=token&client_id=<идентификатор
   приложения>
6. Переносим в env.development.yml токен, логин и uid своего рабочего аккаунта с правами администратора(начинается на
   "yndx-...") (его можно получить если скопировать ссылку Выйти из настроек аккаунта в Метрике (get параметр uid))
7. Запустить проект в watch-режиме:

    `SERVICE_NAME=appmetrica npm run start-service:dev`

    Если нужно запустить отдельно сборку клинета/сборку сервера/сервер следует использовать команды:

    `SERVICE_NAME=appmetrica npm run watch-client`

    `SERVICE_NAME=appmetrica npm run watch-server`

    `SERVICE_NAME=appmetrica npm run start`

8. Сервис доступен по адресу http://localhost:8090/

## Чтобы запустить сервис с использованием авторизации через blackbox и tvm:

1. Указываем конфиг для blackbox:

```yml
...
authConfig:
    shouldUseBlackboxAuth: true
    ...
    blackbox:
        blackboxUrl: http://blackbox-mimino.yandex.net/
        blackboxTvmId: 239
    ...
```

2. Запускаем tvm-tool:

    `YAV_SECRET=sec-01dd1dgwmj1q0qjyskvssz0jhk SECRET_KEY=tvmSecret SOURCE_TVM_ID=2000336 BLACKBOX_TVM_ID=239 API_TVM_ID=2000335 OAUTH_TOKEN=tvmtool-development-access-token PORT=8001 npm run start:tvm-tool`

3. Указываем конфиг для tvm:

```yml
...
authConfig:
    ...
    tvm:
        tvmServiceUrl: '{{DEPLOY_TVM_TOOL_URL}}'
        tvmAuthToken: '{{TVMTOOL_LOCAL_AUTHTOKEN}}'
    ...
```

4. Запускаем сервис с указанием дополнительных переменных окружения

    `DEPLOY_TVM_TOOL_URL=http://localhost:8001 TVMTOOL_LOCAL_AUTHTOKEN=tvmtool-development-access-token SERVICE_NAME=appmetrica npm run start-service:dev`

## Тестовые стенды

Собираются на PR в trunk и релизную ветку. Стенд существует пока PR не будет влит или закрыт, но не более 5 дней.

Стенд можно собрать руками, запустив соответствующий action в CI Арканума.

Subdomain для URL стенда будет сформирован из названия ветки. Например, из ветки `users/john-doe/TASK-100` для сервиса
`Appmetrica`:

```
https://ui-projects-task-100.dev.appmetrica.yandex.ru
```

## Настройка редактора

Если вы используете Visual Studio Code, то пригодятся расширения:

```bash
code --install-extension EditorConfig.EditorConfig
code --install-extension dbaeumer.vscode-eslint
code --install-extension Orta.vscode-jest
```

## Отладка

### Visual Studio Code

Ставим breakpoint, открываем Debugger (`⇧⌘D`), выбираем конфигурацию для нужного вам сервиса (верхняя панель) и жмем
"Start Debugging" (`F5`).

### WebStorm

Создаём конфигурацию для npm скрипта и запускаем в Debug режиме.

### Локализация

Переводы проекта хранятся в [танкере](https://tanker.yandex-team.ru) <br> Для работы с танкером используется
[Tanker-kit](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/tanker-kit/README.md) и локальные скрипты,
которые лежат в `tools/i18n`

-   Для выгрузки переводов из танкера используется команда `i18n:pull`
    ```
    SERVICE_NAME=[SERVICE_NAME] npm run i18n:pull
    ```
-   Для синхронизации переводов используется команда `i18n:sync`
    ```
    SERVICE_NAME=[SERVICE_NAME] npm run i18n:sync
    ```
-   Загрузить новые ключи и обновить старые можно через команду `i18n:merge`
    ```
    SERVICE_NAME=[SERVICE_NAME] npm run i18n:merge
    ```
