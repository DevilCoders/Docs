# MBO Frontend

[![oko](https://badger.yandex-team.ru/oko/repo/market-java/mbo-frontend/health.svg)](https://oko.yandex-team.ru/repo/market-java/mbo-frontend)

Монорепозиторий команды фронтенда MBO

## Примеры/документация

- [mbo-components](https://pages.github.yandex-team.ru/market-java/mbo-frontend/mbo-components/)
- [mbo-parameter-editor](https://pages.github.yandex-team.ru/market-java/mbo-frontend/mbo-parameter-editor/)
- [таска публикации пакетов](https://teamcity.yandex-team.ru/buildConfiguration/Market_Mbo_MboFrontend_MboFrontendPublish?)

Обновление документации: `npm run build:docs && npm run deploy`

## Быстрый старт

Склонируйте репозиторий:

```bash
git clone https://github.yandex-team.ru/market-java/mbo-frontend.git
cd mbo-frontend
```

Установите корневые пакеты:

```bash
npm ci
```

Соберите:

```bash
npx lerna run build
```

## Создать новый пакет

```bash
npm run new-package
```

Генератор запросит ввести имя и описание для нового пакета. После генерации скелет проекта будет в ./packages/${имя_пакета}

Дальше как обычно: коммит, ПР и т.д. После мержа таска опубликует пакет.

#### Для быстрого старта этого достаточно. Ниже читаем, если есть нюансы с зависимостями и т.д.

## Зависимости

В зависимости от того, с каким пакетом вы будете работать, может также возникнуть необходимость сделать сборку. Например, `@yandex-market/mbo-parameter-editor` зависит от `@yandex-market/mbo-components`. Поэтому в `node_modules` у `@yandex-market/mbo-parameter-editor` будет symlink на `@yandex-market/mbo-components`. Сборка каждого пакета происходит командой:

```bash
npm run build
```

Если хотите выполнить команду из корня, то нужно использовать `lerna`:

```bash
npx lerna run build --scope @yandex-market/mbo-components
```

### Описание директорий монорепозиторий

`@types` - пользовательские типы для TypeScript.
`packages` - пакеты, которые публикуются в `npm.yandex-team.ru`

### № Как подключить пользовательские типы из корня

При добавлении `tsconfig.json` внутри пакета, обязательно наследуем его от `.configs/tsconfig.dev.json` или `.configs/tsconfig.prod.json`. Есть одна деталь: `tsconfig.json` не умеет наследовать конфиги из `node_modules`, поэтому нужно указывать относительный путь к файлу.

#### Как добавить зависимость в корень

В конечном итоге в корневом `package.json` должны остаться только `devDependencies`, которые шарятся между большинством пакетов внутри репозитория. Из-за опции [`hoist`][lerna-hoist], при `lerna bootstrap` в `package-lock.json` также добавляются поднятые из пакетов зависимости, которых нет в корневом `package.json`.

В репозиторий закоммичена версия lock-файла с поднятыми зависимостями. Если после клонирования сделать просто `npm install` без `lerna bootstrap`, то появится нежелательный дифф, удаляющий из `package-lock.json` поднятые зависимости.

Поэтому для добавления новых пакетов в корень следует выполнить следующую команду:

```bash
npm install --save-dev --save-exact <зависимости> && npx lerna bootstrap
```

[lerna-hoist]: https://github.com/lerna/lerna/blob/cd5a8fa6b92b25de60ffd0386a9768a158c9eb93/doc/hoist.md

#### Как добавить зависимость в пакет

Если добавляемый пакет нужен для разработки, то его необходимо ставить в корневой `package.json` в `devDependencies`. Но если это консольная утилита и используется в `scripts` пакета, то нужно так же установить его в `devDependencies`. При этом версия в корне должна совпадать с версией в пакете. Это необходимо для того, чтобы `lerna` проставила ссылки внутри пакета на консольные утилиты и можно было выполнять команды через `npm run`, находясь в директории пакета. Если это не сделать, то команды можно будет выполнять только через `npx lerna run` или `npx lerna exec`. После установки пакета, необходимо выполнить команду `npx lerna bootstrap`, чтобы подтянуть зависимости наверх и обновить `package-lock.json`.

#### Если задачи Sandbox'а падают с ошибками, но локально ошибок нет

Помочь понять причину, почему падают задачи, может следующая последовательность команд:

```bash
npx lerna clean -y && npx lerna run clean && npm ci
npx lerna run build
```
Если надо пересобрать отдельный пакет то нужна такая команда:

```bash
npx lerna run build --include-dependencies --scope @yandex-market/mbo-model-rules
```
