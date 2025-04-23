# Error patterns

Библиотека, содержащая возможные типы ошибок hermione. Каждый тип ошибки имеет паттерн, с помощью которого производится группировка ошибок.

Экспортирует массивы объектов:
#### `infrastructureErrorPatterns`:
```js
{
    name: 'string',
    pattern: 'string',
    hint: 'string'
}
```
Используется в:
- [hermione-retry-progressive](https://github.com/gemini-testing/hermione-retry-progressive):
  - для ретраев тестов, падающих с ошибками, которые можно отнести к инфраструктурным.

#### `testErrorPatterns`:
```js
{
    name: 'string',
    pattern: 'string',
    hint: 'string'
}
```

Пока нигде явно не используется.

#### `errorPatterns`:
```js
{
    name: 'string',
    pattern: 'string',
    hint: 'string'
}
```

Состоит из `testErrorPatterns` и `infrastructureErrorPatterns`.

Используется в:

- [html-reporter](https://github.com/gemini-testing/html-reporter):
  - для группировки тестов по типам ошибок;
  - для подмены оригинального сообщения об ошибке на сокращенное/понятное. Первой строкой выводится `name` типа ошибки + оригинальное сообщение за [расхлопушкой](https://developer.mozilla.org/ru/docs/Web/HTML/Element/details);
  - для добавления подсказки (поля `hint`) к ошибкам: что делать и к кому бежать.
- [messier](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/messier):
  - для отправки сматчившихся паттернов в базу данных.
- [testcop(счетовод)](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/services/testcop):
  - для получения сматчившихся паттернов из базы данных и построении статистики на основе этих данных.
