# Монорепозиторий фронта Метрики

[README с полезными ссылочками про Метрику](https://a.yandex-team.ru/arc_vcs/metrika/frontend/front/services/metrika/README.md#metrika-frontend)

### Общее
* Изучить [lerna](https://h.yandex-team.ru/?https%3A%2F%2Flerna.js.org)
* Установить [nvm](https://h.yandex-team.ru/?https%3A%2F%2Fgithub.com%2Fcreationix%2Fnvm) и 12-ю версию nodejs

### Про структуру
Про структуру и работу с зависимостями [написано на вики](https://wiki.yandex-team.ru/jandexmetrika/frontend/frontend_development/#strukturarepozitorija)

### Установка необходимых зависимостей
```bash
npm run bootstrap:<service>
# Например АппМетрика:
npm run bootstrap:appmetrica
```

### Запуск дев сервера
```bash
npx lerna run <command> --scope=<service-name>
# Например АппМетрика:
npx lerna run appmetrica-bem
# NOTE: если команда уникальная на все проекты, то --scope можно не указывать
```

### Как правильно устанавливать, добавлять или удалять зависимости?
Правило простое
* Если нужно установить зависимости при первом чекауте или при подтягивании кода из репозитория с новым пакетом в зависимостях
    * `npm run bootstrap` для установки зависимостей всех проектов
    * `npm run bootstrap -- --scope=<service-name>` - конкретного проекта. Под капотом эта команда вызывает `npm ci`
* Если нужно установить новый пакет, то
    1) `npm i --save[-dev] <package-name>`
    2) Закоммитить изменения вместе с `package-lock.json`

### Именование веток
Ветки именуем следующим образом:
`<your-login>-<task-name>`, например `eduarddyckman-MOBMET-1234`. Это нужно для корректной работы автобет

### Инструкция по работе с данными marketplace
[Подробная инструкция](https://a.yandex-team.ru/arc_vcs/metrika/frontend/front/services/metrika-bem/tools/marketplace-data/README.md#здесь-лежат-данные-для-маркетплейса) — это может вам понадобиться, когда вы дежурный и вас отвлекают словами "маркетплейи и интеграции"
