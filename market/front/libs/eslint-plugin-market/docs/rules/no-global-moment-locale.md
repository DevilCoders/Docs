# no-global-moment-locale

Запрещает задавать язык переводов для momentjs

> Почему?
Не явно задается язык для всего окружения.

## Примеры

Примеры **неправильного** кода:

```js
moment.locale('ru');
moment.locale('en');
moment.locale(someVar);
```

Примеры **правильного** кода

```js
moment().locale('ru');
moment('2020-02-05').locale('en');
moment('2020-02-05T10:29:41.314Z').locale(someVar);
moment(1580898605495).locale(anotherVar);
```
