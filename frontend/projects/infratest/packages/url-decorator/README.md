# @yandex-int/url-decorator

Плагин для [hermione](https://github.com/gemini-testing/hermione/), предоставляющий для запуска тестов на [kotik](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/kotik).
Библиотеки для [gemini](https://github.com/gemini-testing/gemini) и [hermione](https://github.com/gemini-testing/hermione/) для использования в [templar-runner](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/templar-runner)

Заменяет метод `url`, добавляя при запросах два query-параметра.

В параметр с именем, переданным в `suiteId`, будет добавлено значение для обеспечения уникальности кешей репорта. Оно повторяется при повторном запуске теста.

В параметр `testRunId` будет добавлено значение, уникальное для каждого запуска теста. Все url, открытые в рамках одного запуска теста, будут иметь одинаковый `testRunId`. В тесте получить доступ к `testRunId` можно следующим образом:
```
this.browser.executionContext['testRunId']
```

## Установка

```bash
$ npm install @yandex-int/url-decorator --registry http://npm.yandex-team.ru
```

## Конфигурация

* **enabled** (optional) `Boolean` – включение/выключение плагина; по умолчанию плагин включен
* **suiteId** (optional) `String` – имя параметра в урлах тестов, предоствляющего id сьюта; `url-decorator` будет использовать этот id для сохранения уникальных кэшей репорта для каждого теста
* **addCacheInfoToTestRunId** (optional) `Boolean` – добавляет больше информации в testRunId: путь к файлу теста и хэш от фултайтла. Служебное поле, используйте с осторожностью.
* **saveTestRunIdToCookie** (optional) `Boolean` – дополнительно сохраняет `testRunId` в cookie браузера. Это полезно, чтобы после открытия страницы, можно было переходить по ссылкам без дополнительного указания этого параметра.

## Использование

### hermione

Подключить плагин в конфигурационном файле:

```js
// ...

module.exports = {
    // ...

    plugins: {
        '@yandex-int/url-decorator/hermione': {
            // конфигурация
        }
    }
};
```
