# API &middot; [![Build Status](https://drone.yandex-team.ru/api/badges/paskills/api/status.svg)](https://drone.yandex-team.ru/paskills/api)

API for PostgreSQL database with external skills metadata.

The application provides several API endpoints and CLI.

## Initial setup

Install the dependencies.

```
npm install
```

Next, copy `.env.example` to `.env`

Awesome, you're all set!

## Starting the application

In order to run the application one should run several terminal commands in parallel.

You can look search for these commands in `scripts` section of `package.json` file. They're prefixed with `dev:`.

We recommend to use iTerm2 in [split window](https://coderwall.com/p/el3fbg/split-window-with-iterm-2) mode to group all terminals in one window.

### Typescript compiler

Application is written in [TypeScript](typescriptlang.org).

To start the compiler in watch mode run

```bash
npm run dev:build
```

### Tvmtool

[tvmtool](https://wiki.yandex-team.ru/passport/tvm2/qloud/#konsolnyjjklient) is a CLI tool to issue [TVM2](https://wiki.yandex-team.ru/passport/tvm2/) tickets in development environment.

Copy `.tvm.dev.json.example` to `.tvm.dev.json` and set `secret` property. You can get the secret [here](https://abc.yandex-team.ru/services/yandexdialogs2/resources/?search=2000245&state=requested&state=approved&state=granted&view=consuming&show-resource=4546952). If you do not have the access, ask someone from [dev-team](https://abc.yandex-team.ru/services/yandexdialogs2/?scope=development)

Tvmtool is now configured, so you can start it.

```bash
npm run dev:tvmtool
```

### Database

In order to start the database server, Docker is required.

Run the database container.

```bash
npm run dev:db:run
```

If you want to use local PostgreSQL server you should specify it by setting environment

```bash
export PASKILLS_DB_URI=postgres://paskills:paskills@localhost:5432/paskills
export PASKILLS_PG_CONNECTION_STRING='host=localhost port=5432 sslmode=disable dbname=paskills user=paskills password=paskills'
export PASKILLS_PG_SSL_ENABLE=false
```

Create requiring database extensions

```bash
psql ${PASKILLS_DB_URI} -c 'CREATE EXTENSION IF NOT EXISTS "uuid-ossp";'
```

Run database migrations.

```bash
npx sequelize db:migrate
```

To query the database, you can run sql client with the following command.

```bash
npm run dev:db:repl
```

### Node.js server

At last, you need to run the Node.js server.

```bash
npm run dev
```

[magicdev](https://github.yandex-team.ru/toolbox/magicdev) is used under the hood. Application will be available at https://localhost.msup.yandex.ru:8081.

### Генерация классов для работы с Protobuf

Приложение взаимодействует с некоторыми сервисами посредством protobuf. Для удобной генерации классов можно использовать npm скрипт. Скрипт нужно выполнять из корня проекта. Также для генерации нужно установить protocol compiler по данной [инструкции](https://github.com/protocolbuffers/protobuf#protocol-compiler-installation)

```bash
npm run proto:generate -- protos/<name>.proto
```

Где `name` - имя файла в папке `protos`
Сгенерировать можно только один .proto файл за раз.

Сгенерированные классы появятся в директории `src/protos`

### Дебаг тестовых файлов

-   Открываем проект в VS CODE
-   Открываем нужный тестовый файл из директории `src/test` (ava настроена на запуск typescript файлов)
-   При необходимости устанавливаем breakpoint
-   Открываем debug-панель (клик на иконку с жучком на вертикальном меню слева)
-   В выпадающем списке выбираем `Debug AVA test file`
-   Нажимаем Run, либо F5

### Сервис заглушка для облачных функций

`npm run dev:cloud`
