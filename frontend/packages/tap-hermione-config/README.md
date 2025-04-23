# Общий конфиг Hermione для турбоаппов

За основу взят общий [конфиг монорепы frontend](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/packages/frontend-hermione-config/README.md). Что добавлено для турбоаппов:

- Автоматическое поднятие локального http сервера с собранной статикой из директории `build/`, поддержкой History API и CSP.
- Версия мобильного chrome обновлена до `77.0`, так как на более старых версиях нет платформы турбоаппов.
- Настроен мобильный chrome в разрешении 320px, 360px и 414px по ширине и 640px по высоте.
- Подключен набор часто используемых команд, список можно посмотреть в директории `src/commands`.
- Сделана автоматическая очистка Cookie и IndexedDB перед началом теста.
- Настроена авторизация в тестах через [TUS](https://wiki.yandex-team.ru/tus/).
- Настроен запуск с локальным браузером через chromedriver.


## Подключение на проекте

Установить Hermione и этот пакет в проект:
```bash
npm install --save-dev hermione
npm install --save-dev @yandex-int/tap-hermione-config
```

Создать в проекте конфиг `.config/hermione/hermione.conf.js`:
```js
const fs = require('fs');
const path = require('path');

const cspRulesFile = path.join(__dirname, '../../build/csp-rules.txt');
const cspRules = fs.readFileSync(cspRulesFile, { encoding: 'utf-8' });

const config = require('@yandex-int/tap-hermione-config')({
    project: require('../../package.json').name,
    cspRules,
    deletePersistedData: 'indexed-db-name',
    debug: Boolean(process.env.HERMIONE_LOCAL_DEBUG)
});

module.exports = config;
```

В package.json добавить скрипты:
```json
{
    "scripts": {
        "ci:hermione": "npm run build && npm run hermione",
        "build": "...",
        "hermione": "hermione --config ./.config/hermione/hermione.conf.js --retry 3",
        "hermione:gui": "npm run hermione -- gui",
        "hermione:gui:debug": "npm run hermione:gui -- --debug --debug-vnc-before-test 1 --debug-no-timeouts 1",
        "hermione:local:debug": "HERMIONE_LOCAL_DEBUG=1 hermione --inspect --config .config/hermione/hermione.conf.js -b chrome-grid-360"
    }
}
```

## Где запускаются тесты

Во всех окружениях (пул-реквесты и релизы) тесты запускаются с локально собранным турбоаппом. 
Для этого поднимается локальный http сервер, который раздает статику из директории `build/`.

Такое решение позволяет собирать отдельную версию турбоаппа для hermione тестов, а так же использовать тестовое окружение и тестовых пользователей при запуске тестов в релизах. 


## Пользователи

Авторизация в тестах сделана при помощи сервиса [TUS](https://wiki.yandex-team.ru/tus/) и плагина [hermione-auth-commands](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/hermione-auth-commands). 
Полную документацию по командам можно посмотреть в описании плагина.

Для авторизации используется тестовый Паспорт и tus-консумер `tap-team`.

Примеры команд:
```js
// Авторизация одним и тем же пользователем. Подходит для тестов, в которых не меняются данные пользователя.
// Если пользователь не сущестует, то будет создан новый пользователь в тестовом паспорте.
await this.browser.auth('username');

// Создание нового пользователя на каждое выполнение теста. Подходит для тестов, в которых важно иметь чистого пользователя.
await this.browser.authAny(Date.now());

// Получение информации
const user = await this.browser.getMeta('tus');
```

Получить пароль и другую информацию о тестовом пользователе можно через [tus-cli](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/tus-cli#поддерживаемые-команды).

Пример:
```bash
# Все пользователи имею префикс 'yndx-tap-' в логине
tus-cli -c tap-team -e test show --login yndx-tap-username
```


## Дампы HTTP запросов

Параметры запуска hermione для записи и воспроизведения дампов:

- `--save` – запись новых дампов на диск.
- `--play` – воспроизведение ранее записанных дампов. Если дамп для какого-либо запрос не найден, то будет ошибка.
- `--create` – воспроизведение ранее записанных дампов. Если дамп для какого-либо запрос не найден, то он будет создан.


## Отладка тестов

Запуск теста с записью видео:
```bash
hermione:gui -- --debug --debug-record-video 1 --grep test-case-1
```

Запуск теста с доступом до виртуалки через браузер:
```bash
npm run hermione:gui:debug -- --grep test-case-1
```

Запуск теста в локальном браузере:
```bash
npm run hermione:local:debug -- --grep test-case-1
```

