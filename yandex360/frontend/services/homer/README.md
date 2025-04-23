[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=yandex360/frontend/services/homer&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/homer)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=yandex360/frontend/services/homer&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/homer)

# Новый хострут <img src="./.github/homer.png" width="300" align="right"/>

## Запуск dev-версии

```sh
# Установить зависимости.
# Запустить с командой npm run start dev.

cd ~/arcadia/yandex360/frontend/services/homer
npm run prepare-dev
npm start dev
```

Работает по адресам `<HOST>/homer` +
  * `/`
  * `/shortcut/:shortcut`
  * `/message_part`
  * `/app_store`
  * `/subscription_status/{subscribe,unsubscribe}`
  * `/phishing_warning`

### Как сделать `<LOGIN>2.<HOST>/homer` или как настроить еще один инстанс homer
- Склонировать монорепу в `~/www2`
- В результате должен появиться такой путь `~/www2/services/homer`

## Trendbox

Джобы Гомера в сэндбоксе можно увидеть [тут](https://sandbox.yandex-team.ru/tasks?owner=PS-FRONTEND&desc_re=homer&order=-id&limit=20&created=14_days).

Для каждого пулл-реквеста прогоняются тесты в сендбоксе

## Локализация

Обновляется только на qyp.

- Зайдите сюда
https://nda.ya.ru/3SjQY7
и скопируйте токен
- На qyp пропишите токен в env переменную: `export TANKER_TOKEN=***`
- Запустите `npm run update-locales`

#### Сборка

Пакет собирается и катится в [New CI](https://a.yandex-team.ru/projects/mail_frontend/ci/releases/timeline?dir=yandex360%2Ffrontend&id=homer_release).

## Структура

### Настройки

#### `config/services/urls.js`

Симлинк на `.../urls.*.js`.
Тут хранятся адреса бекендов.

#### `config/services/options.js`

Склеивает настройки из `.../options-local.js`, `.../options-custom.js` и `.../options-global.js`.
Первое это стандартные, настройки проекта. Последнее это админские переопределения
из `/etc/yamail/...`.

`.../options-custom.js` это симлинк на `.../options.*.js`. Он даёт возможность переопределить
что-нибудь из `options-local` в зависимоти от окружения. При этом `options-global` всё равно
имеет максимальный приоритет.

#### `config/services/index.js`

Собирает вместе два предыдущих файла.
Даёт возможность переопределить адреса бекендов из админских переопределений.
Создаёт геттеры для опций.

#### `config/index.js`

Симлинк на `config/config.*.js`.
Настройки проекта. В основном код живёт в `config/base.js`, а тут можно до-/пере-определять
какие-нибудь методы и настройки.

### Приложение

#### `app/`

#### `routes/`

  * `routes/*/view/` — собираются webpack-ом в папку `views/`

#### `models/`

#### `services/`

#### `views/`

Скомпилированные шаблоны для серверного рендерига.

#### `public/`

Скомпилированная статика (CSS, JS, картинки).
