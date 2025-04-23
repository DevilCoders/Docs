# middleware-idm-access

### Для чего?
Проверка подлинности запроса от IDM. Проект должен быть развернут
за балансером в Qloud. Балансер запрашивает сертификат пользователя,
разбирает его и складывает содержимое в заголовки запроса
`x-qloud-ssl-issuer` и `x-qloud-ssl-subject`.

Мидлвара `middleware-idm-access` проверяет:
1. Запрос пришел на **правильный хост**. Не все API готовы жить за балансером,
который требует от пользователя сертификат. В большинстве случаев API
открыто для всех пользователей по http. Чтобы злоумышленник не смог
использовать ручки IDM для изменения ролей, проверяем, что
запрос пришел на балансер, который требует сертификат.
2. Сертификат принадлежит IDM. Проверка осуществляется на основании полей
`issuer` и `subject`.

### Как использовать?
```js
// Подключаем мидлвару для проверки запроса
const idmAccess = require('middleware-idm-access')({
    hostname: 'idm.youproject.yandex-team.ru',
    subject: ['C=RU', 'ST=Moscow', 'L=Moscow', 'O=Yandex LLC...'],
    issuer: ['DC=ru', 'DC=yandex', 'DC=ld', 'CN=YandexInternalCA']
});

// Создаем экземпляр koa-сервера
const app = new Koa();
const router = new require('koa-router')();

// Реализуем ручки для интеграции с IDM
router.get('/api/v2/info/', idmAccess, () => {
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

