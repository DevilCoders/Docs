# Быстрый старт

## 1. Установить Palmsync в ваш проект

```bash
npm install @yandex-int/palmsync --registry https://npm.yandex-team.ru
```

## 2. Определиться с расположением сценариев в репозитории проекта

* Если в проекте есть авто-тесты, то целесообразно разместить сценарии рядом с соответствующими авто-тестами.
* Если в проекте еще нет авто-тестов, то стоит разместить там, где планируется потом хранить авто-тест.

Типичная структура проекта:

```
features/
    common/
        some-feature/
            some-feature.hermione.js
            some-feature.testpalm.yml
    desktop/
    touch/
```

## 3. Написать сценарии

Написать сценарии согласно [документации](./yaml-files.md).
Если есть уже написанные авто-тесты, то их все необходимо покрыть сценариями.

## 4. Добавить конфигурацию palmsync

Подробнее про [конфигурацию](./configuration.md).

Минимально необходимая конфигурация проекта:

```js
const {formats} = require('@yandex-int/palmsync');

module.exports = {
    project: 'some-project',

    hermioneConfigPath: '.hermione.conf.js',

    filePatterns: {
        yaml: /\.testpalm\.yml$/,
        hermione: /\.hermione\.js$/
    },

    sets: {
        yaml: {
            desktop: {
                specs: [
                    'features/common/**/*.testpalm.yml',
                    'features/desktop/**/*.testpalm.yml'
                ],
                envs: [{
                    PLATFORM: 'desktop'
                }],
                browsers: ['chrome'],
                baseUrl: '/'
            },
            touch: {
                specs: [
                    'features/common/**/*.testpalm.yml',
                    'features/touch/**/*.testpalm.yml'
                ],
                envs: [{
                    PLATFORM: 'touch'
                }],
                browsers: ['chrome-phone'],
                baseUrl: '/'
            }
        },
    },

    testCaseDecorator(test) {
        test.setField('platform', '{{PLATFORM}}');
    }
};
```

## 5. Подготовить "секреты" для синхронизации

Palmsync для синхронизации использует ряд "секретов", которые необходимо передать через переменные окружения:
* `palmsync_testpalmToken` – [токен TestPalm](./configuration.md#testpalmToken) для выгрузки сценариев.
* `SANDBOX_AUTH_TOKEN` – [токен Sandbox](https://sandbox.yandex-team.ru/oauth) для скачивания ресурсов.

Если в проекте необходима выгрузка скриншотов в S3, то необходимо её настроить согласно [инструкции](./screenshots-upload.md).
После чего надо будет добавить еще несколько секретов через переменные окружения:
* `palmsync_s3MdsAccessKeyId` – Идентификатор (логин) в S3-MDS ([подробнее](./screenshots-upload.md)).
* `palmsync_s3MdsAccessSecretKey` – Пароль в S3-MDS ([подробнее](./screenshots-upload.md)).
* `palmsync_jingToken` – [токен Jing](jing.yandex-team.ru) для выгрузки скриншотов загруженных в jing (подойдет любой портальный токен).

## 6. Подготовить проект в TestPalm

В TestPalm необходимо создать проект согласно [инструкции](https://wiki.yandex-team.ru/testpalm/testpalmdoc/#bystryjjstart).

> Токен указанный в `palmsync_testpalmToken` должен принадлежать только тому пользователю/роботу, у которого есть доступ к проекту в TestPalm.

## 6. Запуск

Подробнее про [CLI](./cli.md).

```
npx palmsync validate
npx palmsync synchronize
```
