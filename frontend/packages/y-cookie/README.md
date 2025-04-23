# y-cookie [![Build Status](https://drone.yandex-team.ru/api/badges/maxpon/y-cookie/status.svg?branch=master&style=flat)](https://drone.yandex-team.ru/maxpon/y-cookie)

Библиотека для работы со значением Y-cookie.

[Описание Y-cookie](https://wiki.yandex-team.ru/cookies/y/).

## Install

```bash
npm install y-cookie --registry=http://npm.yandex-team.ru
```

## Usage

```js
var ycookie = require('y-cookie');

var ys = ycookie.parse('foo.bar#kaomoji.%C2%AF%EF%BC%BC_(%E3%83%84)_%2F%C2%AF')
// {
//   foo: 'bar',,
//   kaomoji: '¯＼_(ツ)_/¯'
// }

var yp = ycookie.parse('1234567890.foo.bar#1234567890.kaomoji.%C2%AF%EF%BC%BC_(%E3%83%84)_%2F%C2%AF')
// {
//   foo: {
//     value: 'bar',
//     expires: '1234567890'
//   },
//   kaomoji: {
//     value: '¯＼_(ツ)_/¯',
//     expires: '1234567890'
//   }
// }
```

## API

### parse(cookie)

Преобразует Y-cookie из строки в объект.  
Возвращает пустой объект в случае некорректности переданного аргумента.

#### cookie

*Required*  
Type: `String`

### stringify(data)

Преобразует Y-cookie из объекта в строку.  
Возвращает `undefined` в случае некорректности переданного аргумента.

#### data

*Required*  
Type: `Object`

## Contribution

Пожалуйста, прочитайте [contribution guide](/CONTRIBUTING.md) перед созданием issue или отправкой пулл-реквеста.

## Tests

```
$ npm test
```
