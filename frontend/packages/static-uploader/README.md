# static-uploader

Пакет загрузки файлов статики в [MDS через S3](https://wiki.yandex-team.ru/mds/s3-api/) для проектов монорепозитория фронтенда и не только.

## Установка

```
npm install --save-dev @yandex-int/static-uploader
```

## Настройка

При запуске static-uploader читает конфигурацию из файла `.config/static/index.js`. Формат такой:

```js
module.exports = {
    /**
     * @type {string} В какой бакет грузить.
     * По умолчанию frontend для YENV=production и frontend-test для YENV=testing
     */
    bucket: 'frontend',
    /**
     * @type {string} Имя сервиса
     * По умолчанию берётся из package.json
     */
    service: 'ugc-pages',
    /**
     * @type {string}
     * Версия. По умолчанию версия из package.json для YENV=production
     * и пулреквест с коммитом при YENV=testing
     */
    version: 'v1.2.3',
    /**
     * @type {boolean} Включено ли проксирование через yastatic.net
     * По умолчанию true для YENV=production и false для YENV=testing
     * Влияет на построение путей staticPath и freezePath
     */
    useYastaticCdn: true,
    /**
     * @type {number} Количество одновременно запущенных потоков
     * По умолчанию 512
     */
    concurrency: 512,

    /** @type {object} Куда грузить обычную статику (css и js) */
    static: {
        /** @type {string} Из какой папки при сборке брать статику */
        path: 'build/static',
        /** @type {string[]} Какие файлы заливать (fast-glob) */
        sources: ['**/*.css', '**/*.js'],
        /**
         * @type {string[]} Какие файлы игнорировать (fast-glob)
         */
        ignore: ['**/*.{gz,br}'],
        /**
         * @type {string} Путь в бакете, в который класть статику
         * По умолчанию в проде <service>/<version>
         * В пулреквестах <service>/<prNumber>/<commit>/static
         */
        target: 'ugc-pages/v1.2.3',
        /**
         * @deprecated
         * @type {boolean} Падать ли если пытаемся залить файл вместо существующего
         * Для продакшена true, для тестинга false.
         * При false файл не будет залит, если уже существует
         */
        denyOverwrite: true,
        /**
         * @type {boolean} Перезаписывает существующие файлы
         * По умолчанию false
         */
        overwrite: false,
        /**
         * Опции для записи файлов
         * @see: https://github.yandex-team.ru/search-interfaces/ci/blob/%40yandex-int/si.ci.s3-client%401.5.6/packages/s3-client/typings/s3client.d.ts
         */
        options?: {
            meta: {
                /* Возможность передать пользовательские мета данные
                *  https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMetadata.html#object-metadata
                */
            }
            expires: Date
        },
    },

    /** @type {object} Куда грузить зафриженную статику (css и js) */
    freeze: {
        /** @type {string} Из какой папки при сборке брать зафриженную статику */
        path: 'build/_',
        /** @type {string[]} Какие файлы заливать (fast-glob) */
        sources: ['**'],
        /**
         * @type {string[]} Какие файлы игнорировать (fast-glob)
         * По умолчанию ['**\/*.{gz,br}']
         */
        ignore: ['**/*.{gz,br}'],
        /**
         * @type {string} Путь в бакете, в который класть статику
         * По умолчанию в проде <service>/_
         * В пулреквестах <service>/<prNumber>/<commit>/_
         */
        target: 'ugc-pages/_',
        /**
         * @deprecated
         * @type {boolean} Падать ли если пытаемся залить файл вместо существующего
         * По умолчанию false, но файл не будет перезаписан
         */
        denyOverwrite: false,
        /**
         * @type {boolean} Перезаписывает существующие файлы
         * По умолчанию false
         */
        overwrite: false,
        /**
         * Опции для записи файлов
         * @see: https://github.yandex-team.ru/search-interfaces/ci/blob/%40yandex-int/si.ci.s3-client%401.5.6/packages/s3-client/typings/s3client.d.ts
         */
         options?: {
            meta: {
                /* Возможность передать пользовательские мета данные
                *  https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMetadata.html#object-metadata
                */
            }
            expires: Date
        },
    },

    /** @type {object} Креденшелы к S3 */
    s3: {
        /** @type {boolean} Использовать публичный URL (.s3.yandex.net) для загруженных файлов */
        usePublicUrl: true,
        /** @type {string} По умолчанию process.env.FRONTEND_S3_ACCESS_KEY_ID */
        accessKeyId: process.env.FRONTEND_S3_ACCESS_KEY_ID,
        /** @type {string} По умолчанию process.env.FRONTEND_S3_SECRET_ACCESS_KEY */
        secretAccessKey: process.env.FRONTEND_S3_SECRET_ACCESS_KEY,
        /** @type {string} По умолчанию продакшен MDS S3 */
        endpoint: 's3.mds.yandex.net',
    },
}
```

## Использование

Залить файлы через cli можно с помощью команды static-uploader:

```bash
YENV=testing HERMIONE_RUN=1 static-uploader
```

Вы можете не строить пути к статике сами, а воспользоваться теми, которые генерирует static-uploader:

```js
const { staticPath, freezePath } = require('@yandex-int/static-uploader');
```

Пути уже будут учитывать переменные окружения `YENV` и `HERMIONE_RUN` и конфигурацию из `.config/static/index.js`.

Например, в конфигурации вебпака можно использовать так:

```js
const { staticPath, freezePath } = require('@yandex-int/static-uploader')

module.exports = {
    entry: './src/index.js',
    output: {
        path: path.resolve('build/static'),
        publicPath: staticPath, // Версионируемая статика
        filename: '[setName].js'
    },
    module: {
        rules: [
            // ...
            {
                test: /\.(png|jpg)$/,
                use: {
                    loader: 'file-loader',
                    options: {
                        name: '[sha1:hash:base58:8].[ext]',
                        outputPath: url => { return `../_/${url}` },
                        publicPath: freezePath // Зафриженная статика
                    }
                }
            }
            // ...
        ]
    }
}
```

Если вы хотите проксировать статику через yastatic, вам нужно заказать у админов yastatic проксирование для вашего бакета.

Опция `useYastaticCdn: true` в конфиге не влияет на место загрузки файлов, а влияет исключительно на формирование путей `staticPath` и `freezePath` для использования в webpack и подобном. По умолчанию опция включена.

```
При useYastaticCdn: true
Путь к файлу build/static/main.js будет построен как
https://yastatic.net/s3/<bucket>/<package_name>/v<version>/main.js

При useYastaticCdn: false
Путь к файлу build/static/main.js будет построен как
https://<bucket>.s3.mds.yandex.net/<package_name>/v<version>/main.js
```

## Откуда загружаются файлы: версионируемая и зафриженная статика

Пакет предполагает, что статика находится в следующих директориях (от корня проекта):

- `build/static` - версионируемая статика.
  Например, файл `build/static/main.js` будет загружен в `https://<bucket>.s3.mds.yandex.net/<package_name>/v<version>/main.js`, где `<package_name>` и `<version>` это имя и версия вашего проекта из `package.json`. При необходимости можно переопределить логику в конфиге.
- `build/_` - зафриженная статика (то есть предполагается, что имя файла это некоторый хеш от его содержимого)
  Например, файл `build/_/2cD33cVv.svg` будет загружен в `https://<bucket>.s3.mds.yandex.net/<package_name>/_/2cD33cVv.svg`. Обратите внимание, в урле не фигурирует версия пакета. Предполагается, что часть зафриженной статики остаётся общая между релизами, и кеш у пользователя не сбрасывается. Поэтому если вы пытаетсь с помощью пакета залить зафриженный файл, и он уже существует в бакете, он не будет перезаписан. Не заливайте во фризы файлы, имя которых не зависит от содержимого — используйте для этого версионируемую статику.

При необходимости эти директории можно переопределить в полях конфигурации `static.path` и `freeze.path`.

## Режимы деплоя (YENV)

При запуске static-uploader необходимо установить переменную окружения `YENV`. Поддерживаются значения `testing` или `production`. Они влияют на папку с версионированием.

- Запуск `YENV=testing static-uploader` подходит для сборки пулреквестов в трендбоксе. В пути используется номер пулреквеста (из переменной окружения `TRENDBOX_PULL_REQUEST_NUMBER`) и хеш коммита (из переменной окружения `env.config`, которая представляет из себя JSON).
  ```
  build/static/main.js будет загружен в
  https://<bucket>.s3.mds.yandex.net/<package_name>/<pr_number>/<commit_sha>/static/main.js

  build/_/2cD33cVv.svg будет загружен в
  https://<bucket>.s3.mds.yandex.net/<package_name>/<pr_number>/<commit_sha>/_/2cD33cVv.svg
  ```
- Запуск `YENV=testing HERMIONE_RUN=1` подходит для заливки статики для бет, в которых запускается гермиона. К обычным путям в тестинге добавляется ещё `/hermione`.
  ```
  build/static/main.js будет загружен в
  https://<bucket>.s3.mds.yandex.net/<package_name>/<pr_number>/<commit_sha>/hermione/static/main.js

  build/_/2cD33cVv.svg будет загружен в
  https://<bucket>.s3.mds.yandex.net/<package_name>/<pr_number>/<commit_sha>/hermione/_/2cD33cVv.svg
  ```
- Запуск `YENV=production` подходит для заливки статики для продакшена.
  ```
  build/static/main.js будет загружен в
  https://<bucket>.s3.mds.yandex.net/<package_name>/v<version>/main.js

  build/_/2cD33cVv.svg будет загружен в
  https://<bucket>.s3.mds.yandex.net/<package_name>/_/2cD33cVv.svg
  ```

## Автоматическое сжатие

Все файлы, кроме *.{png,zip,gz,br} автоматически сжимаются в gz и br и заливаются вместе с исходными файлами.

Если рядом с исходными файлами изначально существует сжатые версии, по умолчанию они будут проигнорированы. Изменить такое поведение можно с помощью опции `ignore` (см. раздел Конфигурация ниже), но это может приводить к багам при заливке (см. https://st.yandex-team.ru/FRONTEND-801).

## Авторизация

Для того, чтобы залить файлы в бакет MDS, нужны секреты Access Key ID и Secret Access Key. Как их получить, написано в [документации к MDS S3](https://wiki.yandex-team.ru/mds/s3-api/authorization/#upravlenieaccesskeys).

По умолчанию static-uploader возьмёт эти креденшелы из переменных окружения

```
FRONTEND_S3_ACCESS_KEY_ID
FRONTEND_S3_SECRET_ACCESS_KEY
```

Переопределить их можно в конфиге `.config/static/index.js` в опциях `s3.accessKeyId` и `s3.secretAccessKey`.

## Запуск в sandbox или trendbox

При запуске в любом CI вам нужно докинуть креденшелы в переменные окружения. Для запуска в sandbox или trendbox сложите креденшелы в [Sandbox Vault](https://sandbox.yandex-team.ru/admin/vault).

Имена «волтов» должны быть `env.FRONTEND_S3_ACCESS_KEY_ID` для Access Key ID и `env.FRONTEND_S3_SECRET_ACCESS_KEY` для Secret Access Key. `env.` в начале нужно, чтобы данные из хранилища подкладывались при выполнении таски как переменные окружения. В поле Owner этих значений нужно указать ту группу, от имени которой вы будете запускать таски.

В конфгие trendbox для запуска тасок должна быть указана эта же группа:

```yml
sandbox:
  vault:
    group: <your_group>
```

## Жизнь в монорепозитории si/frontend

Для каждого сервиса в si/frontend на этапе выполнения задач в trendbox будет запущен скрипт `npm run deploy:static`. Все необходимые переменные будут подготовлены.

Пример запуска из корня монорепозитория:

```console
YENV=testing npx lerna run ci:deploy:static --scope @yandex-int/health
```

Чтобы начать заливать статику, вам достаточно обеспечить сборку статики в папки `build/{static,_}` и добавить в package.json скрипт

```js
"scripts": {
    // ...
    "ci:deploy:static": "static-uploader",
    // ...
}
```

По умолчанию статика сервисов, живущих в монорепозитории, заливается в MDS в бакеты `frontend-test` для `YENV=testing` и `frontend` для `YENV=production`.

В trendbox используются credentials робота [robot-frontend](https://staff.yandex-team.ru/robot-frontend).

**Если нужен свой скрипт деплоя**

В `package.json` можно не использовать общий скрипт деплоя `ci:deploy:static`, можно написать собственную реализацию или вообще не писать `ci:deploy:static`, если деплой не нужен.
