# hermione-testpalm-filter [![Build Status][drone-image]][drone-url]

[Hermione](https://github.com/gemini-testing/hermione) плагин для запуска автоматизированых сценариев на основе ранов в [TestPalm](https://wiki.yandex-team.ru/testpalm/).

* [Основные функции](#Основные-функции)
* [Подключение к проекту](#Подключение-к-проекту)
* [Запуск автотестов](#Запуск-автотестов)
* [Разметка автотестов](#Разметка-автотестов)
* [Какие автотесты будут запущены](#Какие-автотесты-будут-запущены)
* [Доступ к TestPalm API](#Доступ-к-testpalm-api)
* [Настройки плагина](#Настройки-плагина)
* [Разработка плагина](#Разработка-плагина)
* [Вопросы и пожелания](#Вопросы-и-пожелания)


## Основные функции

* Позволяет выбрать набор запускаемых автотестов через интерфейс TestPalm
* [Не проходящие по условиям](#Какие-автотесты-будут-запущены) автотесты будут проигнорированы и не будут запускаться
* Может работать в паре с [hermione-testpalm-reporter](https://github.yandex-team.ru/toolbox/hermione-testpalm-reporter)
* Простое подключение к Hermione в виде плагина
* Требует простой [разметки автотестов](#Разметка-автотестов) для связи с TestPalm


## Подключение к проекту

1. Устанавливаем npm модуль:

```bash
npm install --save --registry https://npm.yandex-team.ru hermione-testpalm-filter
```

2. Подключаем плагин в файле `.hermione.conf.js`:

```js
module.exports = {
    plugins: {
        'testpalm-filter': {
            // ID вашего проекта в TestPalm
            project: 'testpalm-project-id',

            // OAuth токен для доступа к TestPalm API (как его получить написано ниже)
            token: 'testpalm-oauth-token',

            // TestRun ID, который нужно запустить (в примере используем переменную окружения для запуска разных TestRun)
            runId: process.env.TESTPALM_RUN_ID
        }
    }
};
```

3. [Размечаем автотесты](#Разметка-автотестов)


## Запуск автотестов

1. Создаем TestRun в интерфейсе TestPalm. [Что такое TestRun и как его создать](https://wiki.yandex-team.ru/testpalm/testpalmdoc/run/).
2. Копируем TestRun ID из адреса страницы, который имеет следующий вид: `https://testpalm.yandex-team.ru/<проект>/testrun/<ID>`
3. Запускаем автотесты с переменной окружения `TESTPALM_RUN_ID`:

```bash
# Если Hermione установлена локально:
TESTPALM_RUN_ID=5a7b4fd1667f47566fa5de3d ./node_modules/.bin/hermione

# Если Hermione установлена глобально:
TESTPALM_RUN_ID=5a7b4fd1667f47566fa5de3d hermione

# Можно передавать все стандартные опции, например:
TESTPALM_RUN_ID=5a7b4fd1667f47566fa5de3d hermione --retry 0 --system-debug true
```

Вместо переменной окружения `TESTPALM_RUN_ID` можно использовать любой другой способ передачи TestRun ID в конфиг.


## Разметка автотестов

Разметка автотестов необходима чтобы связать автотест с тест-кейсом в TestPalm.

Для разметки автотеста необходимо указывать идентификаторы в формате `<project-id>-<testcase-id>`, где:

* `<project-id>` – идентификатор проекта в TestPalm
* `<testcase-id>` — числовой номер тест-кейса в TestPalm

Идентификатор должен находиться в корневом блоке `describe`:

* Если у вас в автотестах еще не используются блоки `describe`, то необходимо их добавить
* Если в одном автотесте у вас описаны несколько тест-кейсов, то необходимо их разнести по разным автотестам
* Если проверки для одного тест-кейса разбиты по разным автотестам, то нужно разметить все автотесты одинаковым идентификатором

Поддерживается два формата разметки:

1. Через заголовки автотестов:

```js
describe('afisha-frontend-168: Покупка билетов в кино', function () {
    it('Проверяем покупку билетов с авторизацией', function () {
        // Код автотеста...
    });

    it('Проверяем еще что-нибудь', function () {
        // Код автотеста...
    });
});
```

2. Через свойство `testpalmId`:

```js
describe('Покупка билетов в кино', function () {
    this.testpalmId = 'afisha-frontend-168';

    it('Проверяем покупку билетов с авторизацией', function () {
        // Код автотеста...
    });

    it('Проверяем еще что-нибудь', function () {
        // Код автотеста...
    });
});
```


## Какие автотесты будут запущены

Плагин запускает только автотесты, подходящие под следующие условия:

* Автотест правильно размечен идентификатором тест-кейса из TestPalm
* Указанный идентификатор тест-кейса содержится в запускаемом TestRun
* Тест-кейс не выполняется сейчас и не запускался ранее. Успешно пройденные или упавшие тест-кейсы повторно не запускаются.
* Тест-кейс находится в статусе `actual`.

Не попадающие под эти критерии автотесты будут проигнорированы (не будут запущены).


## Доступ к TestPalm API

Для получения информации о наборе сценариев внутри TestRun используется [TestPalm API](https://wiki.yandex-team.ru/testpalm/testpalmdoc/api/).
Для доступа к API необходима авторизация, поэтому нужно получить OAuth токен и указать его в настройках `hermione-testpalm-filter`.

OAuth токен можно получить [по этой ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=6d967b191847496a8a7077e2e636142f).

Затем указать в файле `.hermione.conf.js`:

```js
module.exports = {
    plugins: {
        'testpalm-filter': {
            token: '<OAuth токен>'
        }
    }
};
```


## Настройки плагина

Полный список настроек:

```js
module.exports = {
    plugins: {
        'testpalm-filter': {
            // (optional) Позволяет отключить плагин (например, во время разработки нового автотеста). По умолчанию: true
            enabled: true,

            // (required) ID вашего проекта в TestPalm
            project: 'testpalm-project-id',

            // (required) OAuth токен для доступа к TestPalm API
            token: 'testpalm-oauth-token',

            // (required) TestRun, который нужно запустить
            runId: '5a7b4fd1667f47566fa5de3d',

            // (optional) Адрес TestPalm API.
            apiHost: 'https://testpalm.yandex-team.ru',

            // (optional) Любые опции для запросов в TestPalm API
            requestOptions: {
                timeout: 5000,
                rejectUnauthorized: false
            }
        }
    }
};
```


## Разработка плагина

Запуск unit тестов:

```
npm i
npm test
```

Вывод отладочной информации во время запуска тестов:

```bash
NODE_DEBUG=hermione-testpalm-filter TESTPALM_RUN_ID=5a7b4fd1667f47566fa5de3d hermione
```


## Вопросы и пожелания

За помощью с подключением плагина можно обращаться к [nodge@](https://staff.yandex-team.ru/nodge). Принимаются фича-реквесты.

[drone-url]: https://drone.yandex-team.ru/toolbox/hermione-testpalm-filter
[drone-image]: https://drone.yandex-team.ru/api/badges/toolbox/hermione-testpalm-filter/status.svg
