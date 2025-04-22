# yandex-tinyurl [![Build Status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:%28id:Maps_YandexTinyurl_Tests%29,branch:%3Cdefault%3E/statusIcon)](http://teamcity.yandex-team.ru/viewType.html?buildTypeId=Maps_YandexTinyurl_Tests&branch=%3Cdefault%3E&tab=buildTypeStatusDiv&guest=1)

NPM-модуль для сохранения и получения коротких токенов для ссылок.
Работает с https://wiki.yandex-team.ru/tinyurl

## Установка

```
npm install --registry http://npm.yandex-team.ru yandex-tinyurl
```

## Использование

```javascript
var Tinyurl = require('yandex-tinyurl');
var tinyurl = new Tinyurl();
```

Конструктор `Tinyurl([options])` может принимать следующие опции:

* `{String} [url="http://tinyurl.yandex.net/tiny"]` URL cервиса tinyurl.
* `{String} [origin]` Источник запроса для статистики.
* `{Number} [ipFamily=4]` Семейство ip адресов (4 или 6), используемое для разрешения хоста tinyurl.

### Сохранение ссылки и получение токена

```javascript
// Резолвится коротким токеном для ссылки
tinyurl.store('http://maps.yandex.ru/').then(function (token) {
    console.log(token); // выведет 'CraR4Dxy'
}, function (error) {
    console.log(error);
});
```

### Получение полной ссылки по короткому токену

```javascript
// Резолвится полной ссылкой для токена
tinyurl.retrieve('CraR4Dxy').then(function (url) {
    console.log(url); // выведет 'http://maps.yandex.ru'
}, function (error) {
    console.log(error);
});
```

### Ошибки

Cвойство `error.type` содержит тип ошибки и принимает одно из следующих значений:

Значение              | Описание
---------------       | -------------
`EMPTY_TOKEN`         | Не указан токен.
`INVALID_TOKEN`       | Переданный токен не валиден и не может быть распарсен.
`NOT_FOUND`           | Токен не найден. Указанный токен валиден, но не найден.
`INTERNAL_ERROR`      | Внутренняя ошибка сервиса tinyurl.
`NOT_PARSED`          | Не удалось распарсить ответ. Сервис возвратил ответ неизвестного формата, или ответ не содержит требуемых данных.
`SERVICE_UNAVAILABLE` | Сервис недопуступен. Возможно сервис не ответил в заданный период времени или ответил HTTP-кодом отличным от 200.

## Запуск тестов

```
npm i
npm test
```
