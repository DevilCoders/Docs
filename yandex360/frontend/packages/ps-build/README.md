[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=yandex360/frontend/packages/ps-build&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/packages/ps-build)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=yandex360/frontend/packages/ps-build&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/packages/ps-build)

# PS-BUILD

Утилита для сборки простых проектов.
Хранит в себе знания об основных webpack плагинах.


## Содержание
- [Установка](#Установка)
- [Использование](#Использование)
- [ps-build](#ps-build)
  - [Параметры запуска](#Параметры-запуска)
  - [Параметры сборки](#Параметры-сборки)
- [ps-transpile](#ps-transpile)
- [ps-upload-static](#ps-upload-static)
- [ps-clear-static](#ps-clear-static)
- [Переменные окружения](#Переменные-окружения)


## Установка
```
npm i @ps-int/ps-build --save-dev
```

## Использование
Пакет предоставляет набор утилит для автоматизации жизненного цикла проекта.
Список доступных скриптов приведён ниже.

## `ps-build`
Скрипт собирает проект вебпаком с использованием стандартной конфигурации.

Утилиту нужно прописать в package.json и передать ей [флаги](#Параметры-запуска) или определить [переменные окружения](#Параметры-окружения).
```json
{
    "scripts": {
        "build:dev": "ps-build --dev",
        "build:prod": "ps-build --prod",
    }
}
```

### Параметры запуска

##### `--dev|-d`
Устанавливает `NODE_ENV=development` и конфигурирует сборку для dev окружения.

##### `--prod|-p`
Устанавливает `NODE_ENV=production` и конфигурирует сборку для prod окружения.

##### `--server|-s`
Устанавливает `SERVER_BUILD=1` и конфигурирует сборку как серверную.

##### `--pull-request|-P`
Устанавливает переменную `PULL_REQUEST` — ID pull-request'а для сборки в режиме qa-стенда

##### `--hmr|-h`
Устанавливает `HOT_MODULE_REPLACEMENT=1` и конфигурирует сборку с поддержкой HMR.

##### `--inspect|-i`
Переводит node процесс в режим отладки с остановкой на первой строке (`--inspect-brk`).

##### `--analyze|-a`
Устанавливает `USE_BUNDLE_ANALYZER=1` и включает BundleAnalyzer.

##### `--check-types|-t`
Устанавливает `CHECK_TYPES=1` и включает строгую проверку типов при сборке.

##### `--build-root|-b`
Устанавливает `BUILD_ROOT` и настраивает результат сборки проекта на эту директорию.<br>
Более правильный путь, чем вручную выставлять `webpack.options.output.path`.

##### `--webpack-dev-server|--dev-server`
Запускает сборку через [Webpack DevServer](https://webpack.js.org/configuration/dev-server/)

##### `--debug-config`
Устанавливает `DEBUG_CONFIG=1` и пишет в консоль результирующий сборочный конфиг.

### Параметры сборки
Для расширения поведения сборки на уровне проекта нужно создать файл `webpack.extras.js`.
<br>
Файл экспортирует из себя функцию следующего содержания:
```js
module.exports = function(env) {
    return {
        options: {
            runtime: Boolean, // Выделять ли webpack runtime в отдельный chunk
            publicManifest: string | Boolean, // Создавать ли manifest.json в результате сборки
            serverManifest: Boolean | {
                name: string, // (default: 'manifest')
                manifestName: string, // (default: '[name].json')
                runtimeName: string, // (default: '[name].js')
                watchJson: Boolean, // (default: isDev)
                resolveModules: Boolean, // (default: isServer)
                omitRuntimeFiles: Boolean, // (default: isServer)
            },
            withCompression: Boolean, // Сжимать ли файлы в prod сборке
            chunkNamingPattern: string,
            externalCss: string[],
        },
        config: {} // webpack конфиг, кодорый наложится на базовый с помощью webpack-merge
    }
}
```

## `ps-transpile`

TODO: описать скрипт


## `ps-upload-static`
Загружает статику проекта в S3 по конвенции.
- Всегда загружает в bucket `s3://psf/`
- Название директории берётся из названия проекта в `package.json`, не учитывая scope проекта, так проект
`@my-scope/some-project` ляжет в директорию `s3://psf/some-project`
- Будучи запущенным в режиме pull-request'а, с флагом `-pr|--pull-request` или переменной окружения `PULL_REQUEST` кладёт статику в директорию `s3://psf/some-project/__pr__/${PULL_REQUEST}/`. Позднее для очистки статики на закрытии pull-request'а можно воспользоваться скриптом `ps-clear-static`
- Для загрузки по умолчанию использует общий ключ секретницы

### Параметры запуска и окружения
#### `--root|-r`
корень собираемого пакета, по-умолчанию директория, откуда запущен скрипт

##### `--build-root|-b`
Директорию, в которую был собран проект, соответствует аналогичной опции `ps-build`

#### `--inspect|-i`
Переводит node процесс в режим отладки с остановкой на первой строке (`--inspect-brk`).

#### `--secret`
Устанавливает переменную `VAULT_SECRET_UUID` — ID секретов для загрузки статики, по умолчанию используется общий ключ для `psf`

#### `--pull-request|-P`
Устанавливает переменную `PULL_REQUEST` — ID pull-request'а для сборки в режиме qa-стенда

#### `*`
Остальные параметры будут переданы напрямую скрипту `s3cmd`, выполняющему загрузку

## `ps-clear-static`
Удаляет статику pull-request'а из S3.

_Работает только в режиме `PULL_REQUEST`'а, иначе выбрасывает ошибку_

- Обязательно запускать с флагом `--pull-request|-P` или переменной окружения `PULL_REQUEST`. Скрипт рекурсивно удаляет директорию `s3://psf/some-project/__pr__/${PULL_REQUEST}/`
- Название директории определяется аналогично `ps-upload`
- Для загрузки по умолчанию использует общий ключ секретницы

### Параметры запуска и окружения
#### `--root|-r`
корень собираемого пакета, по-умолчанию директория, откуда запущен скрипт

#### `--inspect|-i`
Переводит node процесс в режим отладки с остановкой на первой строке (`--inspect-brk`).

#### `--secret`
Устанавливает переменную `VAULT_SECRET_UUID` — ID секретов для загрузки статики, по умолчанию используется общий ключ для `psf`

#### `--pull-request|-P`
Устанавливает переменную `PULL_REQUEST` — ID pull-request'а для сборки в режиме qa-стенда

#### `*`
Остальные параметры будут переданы напрямую скрипту `s3cmd`, выполняющему загрузку

## Переменные окружения

Переменные окружения влияют на поведение всех утилит из пакета. Подробнее см. описание каждой утилиты.

- `NODE_ENV=development` (development / production)
- `SERVER_BUILD=0` ( 0 / 1 )
- `DEV_SERVER=0` ( 0 / 1 )
- `HOT_MODULE_REPLACEMENT=0` ( 0 / 1 )
- `TEST=0` ( 0 / 1 )
- `CI=0` ( 0 / 1 )
- `USE_BUNDLE_ANALYZER=0` ( 0 / 1 )
- `DEBUG_CONFIG=0` ( 0 / 1 )
- `CHECK_TYPES=0` ( 0 / 1 )
- `PULL_REQUEST=1234` (pull request id)
- `BUILD_ROOT=./build` ( absolute / relative to project path )
- `EXTRAS_CONFIG=./webpack.extras.js` ( absolute / relative to project path )
- `BABEL_CONFIG=./babel.config.js` ( absolute / relative to project path )
- `POSTCSS_CONFIG=./postcss.config.js` ( absolute / relative to project path )
- `TS_CONFIG=./tsconfig.json` (absolute / relative to project path)
