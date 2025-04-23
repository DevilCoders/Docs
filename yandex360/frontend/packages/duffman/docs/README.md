# Duffman

### Запуск сервера
Основная точка входа в сервер это скрипт `bin/www`.

Здесь мы формируем конфиг для [luster] и собственно запускаем его. Luster — это удобная обертка над nodejs [cluster],
которая была выбрана как легковесная альтернатива [pm2]. Основная используемая фича — при перезапуске воркеров за ними
сохраняется их id, что позволяет однозначно определять для каждого воркера TCP порт, на котором он должен слушать.

Luster запускает несколько инстансов `app.js`. Каждый инстанс запускает [express] сервер, подключает к нему основные middleware.
Настройка дополнительных middleware происходит внутри роутеров. Так например не всем роутерам интересно парсить тело запроса,
поэтому [body-parser] мы подключаем только в нужном роутере.

Сами роутеры подключаются через конфиг, который передается в [настройках](./cli.md) при запуске сервера.
```
node bin/www --routes $PWD/duffman-routes/
```
Пример конфига:
```js
const path = require('path');

module.exports = {
    routes: [{
        name: '/u2709/api/models',
        path: path.resolve('./routes/models')
    }]
};
```
Каждый роутер загружает необходимые ему _модели_ и необходимые для моделей _сервисы_.

Итак `bin/www → app.js → routes → models → services`.

### Создание роутера
Роутер представляет из себя функцию принимающую от express два параметра `router(req, res)`.
На основе этих двух параметров можно проинициализировать [ядро](./core.md) duffman-а.
```js
class ExtraCore extends duffman.Core {}
const core = new ExtraCore(req, res);
```

После инициализации ядра к нему нужно подключить модели и сервисы:
```js
const models = require('./models');
const services = require('./services');

class ExtraCore extends duffman.Core {
    constructor(req, res) {
        super(req, res);

        this.models = models;
        this.services = services;
    }
}

// или так
class ExtraCore extends duffman.Core {
    static models = models;
    static services = services;
}
```
В данном случае мы подключили все модели и сервисы объявленные в duffman-е

Теперь ядро нужно авторизовать (`core.auth.set(auth)`). Способ получения авторизации остается на усмотрение программиста.
Обычно это специальная модель `auth`.

После авторизации ядра должны стать доступны для запроса остальные объявленные модели. Доступность запроса определяется
с помощью валидации XSRF токена. Рекомендовано защищать XSRF токеном модифицирующие запросы, но duffman защищает все.
Токен гененрируется в соответствии с [рекомендациями СИБ](https://wiki.yandex-team.ru/security/for/web-developers/csrf/#kakgenerirovatiproverjattoken).
Для других сервисов способ составления и валидации ckey можно переопределить:
```js
class CustomCkey extends duffman.Ckey {
    ...
}

class ExtraCore extends duffman.Core {
    constructor(req, res) {
        super(req, res, { Ckey: CustomCkey });
    }
}
```

### POSIX логирование
Все логи duffman-а направлены через POSIX в syslog. Написан абстрактный класс [AbstractLogger](./abstract-logger.md) от которого
наследуются `core.console` и `http-log`.

Для логирования дополнительных параметров в `core.console` необходимо при инициализации ядра переопределить функцию `logCommonArgs`.
Пример:
```js
class ExtraCore extends duffman.Core {
    logCommonArgs(options) {
        const auth = core.auth.get();
        const config = core.config;

        return Object.assign(options || {}, {
            x_real_ip: config.USER_IP,
            x_request_id: config.REQUEST_ID,
            host: config.HOST,

            uid: auth.uid || core.params._uid || core.params.uid
        });
    }
}
```

Для логирования дополнительных параметров в `http-log` необходимо при инициализации ядра переопределить функцию `httpCommonArgs`. Пример:
```js
class ExtraCore extends duffman.Core {
    httpCommonArgs(options) {
        const auth = core.auth.get();

        // Пробрасываем дополнительные параметры для http лога
        options._http_log = {
            x_real_ip: core.config.USER_IP,
            x_request_id: core.config.REQUEST_ID,
            host: core.config.HOST,

            uid: auth.uid || core.params._uid || core.params.uid
        };

        return options;
    }
}
```

Так же оба этих лога (но не `AbstractLogger`) дополнительно логируют содержание переменной окружения `DUFFMAN_CUSTOM_LOG_ARGS`.

  [luster]: https://github.com/nodules/luster
  [cluster]: https://nodejs.org/dist/v8.12.0/docs/api/cluster.html
  [pm2]: https://github.com/Unitech/pm2
  [express]: https://github.com/expressjs/express
  [body-parser]: https://github.com/expressjs/body-parser
