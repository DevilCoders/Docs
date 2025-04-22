# Тесты

Все тесты запускаются прогоняются на [Mocha](http://visionmedia.github.io/mocha/)
с [Expect.js](https://github.com/LearnBoost/expect.js/) и [Sinon.js](http://sinonjs.org/docs/)


Серверные тесты лежат в `./server` и запускаются моккой напрямую.

Клиентские тесты лежат в `./client` и запускаются в [Phantom.js](http://phantomjs.org/) с помощью [Karma](http://karma-runner.github.io/)


## Файловая структура

Файловая структура в тестах должна повторять структуру основного кода.

Для каждого файла с тестами в `test/client` и `test/server` должен быть соответствующий ему файл без этих приставок.
Например, `test/client/blocks/control/captcha/captha.js` тестирует соответствующий файл `blocks/control/captcha/captha.js`
