# @yandex-market/hermione-broken-tests

Плагин генерирует отчет со списком упавших тестов и умеет запускать только тесты из этого отчета

## config

добавить в ginny.conf

```js
module.exports = {
  // ...
  brokenTests: {
    // плагин включен/выключен
    // true/false
    enabled: true,

    // режим работы плагина
    // - collect - собирает отчет
    // - filter - запуск тестов с фильтрацией из отчета
    mode: 'collect',

    // директория для сохранения/чтения отчета
    reportDir: 'spec/hermione/reports',

    // имя файла отчета
    // по умолчанию = broken-tests.json
    reportFilename: 'broken-tests.json',
  }
}
```

## отчет

в отчете названия тест-кейсов построчно

```
Страница отзывов на магазин. only root siute. test suite. test case fail 1
Страница отзывов на магазин. only root siute. test suite. test case fail 2
```
