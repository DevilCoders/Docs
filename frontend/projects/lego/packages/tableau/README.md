# tableau

Данные для Табло сервисов (Tableau).

```js
const tableau = require('@yandex-lego/tableau');

// Получить JSON-данные для пресета `ru`, языка и домена по умолчанию:
tableau.toJSON('ru');

// Получить JSON-данные для пресета `ru`, турецкого языка и домена по умолчанию:
tableau.toJSON('ru', 'tr');

// Получить JSON-данные для пресета `ru`, турецкого языка и украинского домена:
tableau.toJSON('ru', 'tr', 'ua');

// Получить JSON-данные для пресета `ru`, языка и домена по умолчанию и поискового запроса:
// `id вашего сервиса` нужно для формирования ссылки на Маркет.
// Последний аргумент необязателен, если в вашем Табло нет Маркета.
tableau.toJSON('ru', null, null, 'search query', {serviceId: 'id вашего сервиса'});

// Получить HTML-строку с ссылками:
tableau.toHTML('ru', null, null, 'search query', {serviceId: 'id вашего сервиса'});
```
