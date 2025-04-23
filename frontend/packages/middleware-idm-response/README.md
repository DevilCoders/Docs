# middleware-idm-response

### Для чего?
При интеграции с IDM необходимо возвращать ответ в определённом формате:
  - в случае успеха добавлять в тело ответа `{ code: 0 }`
  - в случае ошибки возвращать ответ с кодом 200 и ошибкой в теле ответа.
    Если повторный запрос может исправить ошибку, то в тело ответа добавляется
    `{ code: 1, error: 'Internal server error' }`. Если повторный запрос не поможет,
    то ответ должен содержать `{ code: 1, fatal: 'Entity not found' }`
Подробнее о формате ответа можно почитать в [документации IDM](https://wiki.yandex-team.ru/Intranet/idm/API/#examples).

Мидлвара `middleware-idm-response` принимает объект с опцией `logger`, которая
должна иметь метод `error` для логгирования ошибок (по умолчанию используется `console`).

### Как использовать?
```js
// Подключаем мидлвару для унификации ответа
const idmResponse = require('middleware-idm-response')({
    logger: console
});

// Создаем экземпляр koa-сервера
const app = new Koa();
const router = new require('koa-router')();

// Реализуем ручки для интеграции с IDM
router.get('/api/v2/info/', idmResponse, () => {
    const roles = {
        slug: 'group',
        values: {
            moderator: 'модератор',
            admin: 'администратор'
        }
    }

    return { roles };
});

// Запускаем сервер
app.listen(80);
```
