# express-cloud-blackbox

```js
const config = {
    // опции блэкбокса
    // @see https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/express-blackbox
    blackbox: {
        // ...blackboxOptions
    },
    // запрос доступов к preprod-хостам Облака: https://puncher.yandex-team.ru
    hosts: {
        // [опционально; по умолчанию - из объекта запроса]
        // хост приложения
        // (например, tracker.yandex.ru)
        app,
        // @see https://wiki.yandex-team.ru/cloud/iamrm/cookbook/endpoints-servisov/#oauth
        authServer,
        // @see https://wiki.yandex-team.ru/cloud/iamrm/cookbook/endpoints-servisov/#tokenservice
        tokenService,
        // @see https://wiki.yandex-team.ru/cloud/iamrm/cookbook/endpoints-servisov/#sessionservice
        sessionService,
        // хост, который указывается в пэйлоуде при запросе IAM-токена;
        // пока для препрода здесь нужно указать продовый хост
        // (iam.api.cloud.yandex.net)
        aud,
        // [опционально; нужен для запроса атрибута 1017 (в режиме без hosts.blackboxEmu)]
        // хост Директории для получения списка организаций
        // (api-internal-test.directory.ws.yandex.net)
        directory,
    },
    // клиент приложения в Облаке
    // запрос: https://forms.yandex-team.ru/surveys/50515/
    client: {
        id,
        password,
    },
    // полный URL или относительный путь роута приложения, на который Облако будет
    // редиректить пользователей для завершения аутентификации и выставления
    // сервисной куки (например, /cloud_auth_callback);
    // этот адрес обрабатывается в этой миддлваре, приложению не нужно его обрабатывать отдельно;
    // этот адрес нужно зарегистрировать на стороне Облака (через разработчиков Облака)
    callbackUrl,
    // опциональный коллбек процесса аутентификации пользователя
    // вызывается вместо стандартной функции аутентификации
    // в качестве аргументов получает (req, res, next, authorize),
    // где authorize(req, res) - исходная функция аутентификации (выполняет редирект пользователя)
    authorizeHandler,
    // спец роут приложения (относительный путь), на котором будет выполняться аутентификация
    // федеративных пользователей через Облако
    // (например, /federations/; тогда аутентификация будет на адресах вида /federations/<federation_id>)
    federationRoute,
    // относительный путь, который будет использоваться для логаута
    logoutRoute,
    // путь к файлу корневого сертификата
    // (например, /usr/local/share/ca-certificates/YandexInternalRootCA.crt)
    cert,
    // сервисный аккаунт Облака;
    // создание: https://cloud.yandex.ru/docs/iam/operations/sa/create
    // для сервисов Коннекта можно запросить аккаунт в облаке Коннекта (через @smosker)
    serviceAccount: {
        id,
        // авторизованный ключ сервисного акаунта Облака;
        // создание: https://cloud.yandex.ru/docs/iam/operations/authorized-key/create
        key: { id, pem },
    },
    tvm: {
        // [если указан hosts.directory]
        // сервис-тикет Директории или функция от (req, res) для его получения
        // (например, req => req.tvm.tickets.directory.ticket)
        directory,
    },
    // [опционально; по умолчанию - 'https']
    // протокол приложения
    protocol,
    // [опционально] id запроса или функция от (req, res) для его получения
    // (например, req => req.requestId)
    requestId,
    // [опционально] callback логирования.
    // (например, (message, level, req) => console.log(message))
    // level может принимать значения 'debug', 'info', 'warn', 'error'
    // req может отсутствовать, это значит что callback вызван не в контексте запроса
    onLogEvent,
    // таймаут, на основе которого вычисляется дедлайн для grpc
    // https://grpc.github.io/grpc/node/grpc.Client.html#~CallOptions__anchor
    timeout,
};

app.use(expressCloudBlackbox(
    config,
    // [опционально]
    // миддлвара, которая будет использоваться в отсутствие облачной сессионной куки yc_session
    // везде, кроме спец роутов callbackUrl и federationRoute
    // (например, expressBlackbox(blackboxOptions))
    fallbackMiddleware,
));
```

Результат этой миддлвары записывается в `req.blackbox` в формате блэкбокса c дополнительным полем `source: 'cloud'`.

## Legacy-настройки

_(для совместимости с более ранним интерфейсом)_

```js
const config = {
    // ...
    hosts: {
        // [опционально] хост облачного эмулятора блэкбокса (бб-эму);
        // эмулятор блэкбокса использует опции блэкбокса из поля blackbox,
        // но поддерживает только метод sessionid;
        // заменён аутентификацией напрямую через SessionService Облака
        // (bb.private-api.cloud-preprod.yandex.net:8654)
        blackboxEmu,
        // хост IAM API Облака
        // (например, iam.api.cloud-preprod.yandex.net)
        // заменён на hosts.tokenService
        iam,
        // ...
    },
    // ...
};
```

## Ссылки

- [API аутентификации Облака](https://wiki.yandex-team.ru/cloud/iamrm/services/API-autentifikacii-Oblaka/?API-autentifikacii-Oblaka#obshhajamexanika)
- [express-blackbox-emu](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/packages/express-blackbox-emu)
