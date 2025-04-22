# hermione-testpalm-reporter [![Build Status][drone-image]][drone-url]

[Hermione](https://github.com/gemini-testing/hermione) плагин для отправки отчетов о запуске автотестов в [TestPalm](https://wiki.yandex-team.ru/testpalm/).

* [Основные функции](#Основные-функции)
* [Подключение к проекту](#Подключение-к-проекту)
* [Запуск автотестов](#Запуск-автотестов)
* [Разметка автотестов](#Разметка-автотестов)
* [Доступ к TestPalm API](#Доступ-к-testpalm-api)
* [Настройки плагина](#Настройки-плагина)
* [Разработка плагина](#Разработка-плагина)
* [Вопросы и пожелания](#Вопросы-и-пожелания)


## Основные функции

* Автоматически выставляет статусы `PASSED` или `FAILED` по результатам выполнения автотестов
* Пишет комментарии о всех этапах выполнения автотестов ([Пример](https://jing.yandex-team.ru/files/nodge/new_hermione__TestPalm_2018-02-14_03-01-58.png))
* При падении автотеста пишет комментарий с версией браузера, описанием ошибки, скриншотом и адресом страницы ([Пример](https://jing.yandex-team.ru/files/nodge/new_hermione__TestPalm_2018-02-14_03-04-01.png))
* Позволяет следить за ходом выполнения автотестов, так как отправляет статусы по мере их выполнения
* Может работать в паре с [hermione-testpalm-filter](https://github.yandex-team.ru/toolbox/hermione-testpalm-filter)
* Простое подключение к Hermione в виде плагина
* Требует простой [разметки автотестов](#Разметка-автотестов) для связи с TestPalm
* Работает с автотестами без разметки, такие автотесты не попадают в отчет в TestPalm


## Подключение к проекту

1. Устанавливаем npm модуль:

```bash
npm install --save --registry https://npm.yandex-team.ru hermione-testpalm-reporter
```

2. Подключаем плагин в файле `.hermione.conf.js`:

```js
module.exports = {
    plugins: {
        'testpalm-reporter': {
            // ID вашего проекта в TestPalm
            project: 'testpalm-project-id',

            // OAuth токен для доступа к TestPalm API (как его получить написано ниже)
            token: 'testpalm-oauth-token',

            // TestRun ID, в который нужно отправить отчет (в примере используем переменную окружения для запуска разных TestRun)
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

Идентификатор может находиться в любых блоках `describe` или `it`:

* Если размечен блок `describe`, то все вложенные в него автотесты будут автоматически размечены тем же идентификатором
* В одном файле могут находиться несколько автотестов с разными идентификаторами
* Один и тот же идентификатор можно указывать несколько раз, тогда результат всех автотестов будет привязан к одному тест-кейсу

Поддерживается следующие форматы разметки:

1. Через заголовки в блоках `describe`:

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

2. Через заголовки в блоках `it`:

```js
it('afisha-frontend-168: Проверяем покупку билетов с авторизацией', function () {
    // Код автотеста...
});
```

3. Через свойство `testpalmId` в блоке `describe`:

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

4. Через свойство `testpalmId` в блоке `it`:

```js
it('Проверяем покупку билетов с авторизацией', function () {
    this.testpalmId = 'afisha-frontend-168';

    // Код автотеста...
});
```


## Доступ к TestPalm API

Для выставления статусов тест-кейсов используется [TestPalm API](https://wiki.yandex-team.ru/testpalm/testpalmdoc/api/).
Для доступа к API необходима авторизация, поэтому нужно получить OAuth токен и указать его в настройках `hermione-testpalm-reporter`.

OAuth токен можно получить [по этой ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=6d967b191847496a8a7077e2e636142f).

Затем указать в файле `.hermione.conf.js`:

```js
module.exports = {
    plugins: {
        'testpalm-reporter': {
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
        'testpalm-reporter': {
            // (optional) Позволяет отключить плагин (например, во время разработки нового автотеста). По умолчанию: true
            enabled: true,

            // (required) ID вашего проекта в TestPalm
            project: 'testpalm-project-id',

            // (required) OAuth токен для доступа к TestPalm API
            token: 'testpalm-oauth-token',

            // (required) TestRun, в который нужно отправить отчет
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
NODE_DEBUG=hermione-testpalm-reporter TESTPALM_RUN_ID=5a7b4fd1667f47566fa5de3d hermione
```


## Вопросы и пожелания

За помощью с подключением плагина можно обращаться к [nodge@](https://staff.yandex-team.ru/nodge). Принимаются фича-реквесты.

[drone-url]: https://drone.yandex-team.ru/toolbox/hermione-testpalm-reporter
[drone-image]: https://drone.yandex-team.ru/api/badges/toolbox/hermione-testpalm-reporter/status.svg
