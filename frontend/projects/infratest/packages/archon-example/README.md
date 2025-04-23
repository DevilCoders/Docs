# archon-example

Проект-пример для демонстрации возможностей [Archon].

Код примера находится в [аркадии](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-example).

Настройка проекта начинается с добавления зависимости от `@yandex-int/archon` в `package.json` и продолжается
описанными ниже шагами.

## 1. Добавление `.yproject`

Данный файл обозначает корень проекта и содержит различные проектные настройки в виде JSON.
В нашем проекте мы указываем [в нём](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-example/.yproject) в свойстве `paths.archon` путь до папки с конфиругацией [Archon]:

```json
{
    "paths": {
        "archon": "./configs/archon"
    }
}
```

## 2. Добавление конфигурации [Archon] 

Создаём директорию с конфигурацией [Archon] в соответствии с тем, что мы указали в `.yproject`. 

В ней создаём `config.json` и указываем в нем поле `commands`, пока пустое:

```json
{
    "commands": [
    ]
}
```

## 3. Создание простейшей команды (aka "Hello, World!")

В директории `configs/archon` создаем папку [`commands`](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-example/configs/archon/commands), а в ней [`hello-command.js`](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-example/configs/archon/commands/hello-command.js) со следующим содержимым:

```js
'use strict';

module.exports = {
    name: 'say-hello',
    description: 'Greet user',
    setup(command) {
        return command
            .options({
                user: {
                    alias: 'u',
                    type: 'string',
                    description: 'Имя пользователя',
                    requiresArg: true
                }
            });
    },
    graph(options) {
        return [
            {
                name: 'hello-username',
                async init() {
                    console.log(`Hello ${options.user || process.env.USER}, this is the most simple Archon component!`);
                }
            }
        ];
    }
};
```

В экспортируемом объекте команды мы видим следующие поля:

* `name` - название команды, в [Archon] CLI будет использовано именно оно;
* `setup` - настройка команды commander, в данном случае, задание описания и одной опции;
* `graph` - настройка графа компонент команды с использованием опций, в данном случае, в графе всего один inline-компонент с именем `hello-username`.

В данном примере компонент описан прямо в файле с командой. `hello-username` - простой компонент, который
при активации (вызове `init`) выводит в консоль строку-приветствие с именем пользователя из опции или из окружения и завершается.

Таким образом, команда в целом просто выводит строку в консоль и завершает выполнение.

Теперь добавляем команду в конфигурацию [Archon], и можем её запускать:

```json
{
    "commands": [
        "./commands/hello-command"
    ]
}
```

```
$ archon say-hello -u archon
Hello archon, this is the most simple Archon component!
```

## 4. Создание полезной команды, стартующей сервер, раздающий статику

В этом примере будет опять же один компонент, но на этот раз он будет делать полезное дело - раздавать статику по HTTP.

В директории `configs/archon` создаем папку [`components`](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-example/configs/archon/components) и в ней [`static-server.js`](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-example/configs/archon/components/static-server.js):

```js
'use strict';

const connect = require('connect');
const serveStatic = require('serve-static');

module.exports = class StaticServer {
    constructor({name = 'static-server', httpPort}) {
        this.name = name;
        this.httpPort = httpPort;
        this.httpServer = null;
    }

    async init(results, done) {
        return new Promise((resolve, reject) => {
            const app = connect();
            app.use(serveStatic('static', {'index': 'index.html'}));

            this.httpServer = require('http').createServer(app).listen(this.httpPort, () => {
                console.error(`Static server started on http://localhost:${this.httpPort}`);
                resolve({httpPort: this.httpPort});
            });
            this.httpServer.on('error', (error) => {
                if (this.httpServer.listening) {
                    // ошибка при запущенном сервере, запускаем деактивацию
                    done(error);
                } else {
                    // ошибка при запуске сервера, reject останавливает активацию и вызывает деактивацию
                    reject(error);
                }
            });
        });
    }

    async shutdown() {
        await new Promise((resolve) => {
            if (this.httpServer) {
                this.httpServer.close(resolve);
            } else {
                resolve();
            }
        });
    }
};
```

Данный компонент, в отличие от предыдущего примера, является долгоживущим, поэтому для него важно задать поведение не
только на активацию, но и на деактивацию.

* Активация запускает сервер. На вход `init` получает `results` и `done`. `StaticServer` не зависит от других компонентов,
поэтому `results` использоваться не будет. А вот `done` - будет. Если произойдет ошибка при запуске или работе сервера,
то нам нужно будет остановить выполнение команды, и для этого будет вызван `done` с аргументом-ошибкой.
Promise `init` резолвится в тот момент, когда сервер начинает слушать. При резолве возвращается порт, на котором поднялся сервер. 
* Деактивация произойдет при останове команды пользователем или при ошибке во время инициализации или жизни процесса
сервера. При этом есть два обработчика завершения компонента: `shutdown` и более экстренный `terminate`. Здесь мы
определим только первый - `shutdown` - останавливающий запущенный сервер.

Теперь нужно реализовать команду, которая этот сервер будет запускать. Также мы хотим иметь возможность задавать порт
через опцию нашей команды. Создаём файл [`static-server.js`](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-example/configs/archon/commands/static-server.js):

```js
'use strict';

const StaticServer = require('../components/static-server');

module.exports = {
    name: 'serve-static',
    description: 'Start static server',
    setup(command) {
        return command
            .options({
                'http-port': {
                    alias: ['p'],
                    type: 'number',
                    description: 'HTTP port',
                    requiresArg: true,
                    default: 3333
                }
            });
    },
    graph(options) {
        return [
            new StaticServer({
                name: 'server',
                httpPort: options.httpPort
            })
        ];
    }
};
```

Мы создали команду `serve-static`, определили для нее описание и опцию `--http-port` с дефолтным значением `3333`. Граф
компонент при этом состоит из одного элемента - нашего сервера. Мы переопределили ему имя и передали порт в конструктор.

Теперь добавляем команду в конфигурацию [Archon] и запускаем:
```json
{
    "commands": [
        "./commands/static-server"
    ]
}

```

```
$ archon serve-static
Static server started on http://localhost:3333
```

И по адресу http://localhost:3333 можно увидеть [статическую страницу с котиком](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-example/static/index.html).

## 5. Создание полезной команды, стартующей сервер, раздающий статику, с поддержкой HTTPS

До этого мы создавали команды, использующие всего один компонент. Пришло время более сложных команд! На этот раз мы
создадим команду, запускающую сервер, аналогичный предыдущему, но поддерживающий HTTP и HTTPS.

Для этого нам понадобится подключить сторонний модуль с готовым компонентом для [Archon] - [`@yandex-int/internal-cert`](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon_pakety_s_komponentami_i_komandami/internal-cert.html).

Компонент сервера похож на компонент из предыдущего примера (находится [тут](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-example/configs/archon/components/static-server-https.js)),
но зависит от готового компонента `cert` и использует оставленные им выходные данные для настройки HTTPS-сервера:

```js
'use strict';

const connect = require('connect');
const serveStatic = require('serve-static');

const fs = require('fs');
const tls = require('tls');

function createHttpsOpts(certOpts) {
    ...
}

module.exports = class StaticServer {
    constructor({name = 'static-server', deps, transformInput, httpPort, httpsPort}) {
        this.name = name;
        this.deps = deps;
        this.transformInput = transformInput;

        this.httpPort = httpPort;
        this.httpsPort = httpsPort;

        this.httpServer = null;
        this.httpsServer = null;
    }

    async init(results, done) {
        const cert = results.cert;
        return new Promise((resolve, reject) => {
            const app = connect();
            app.use(serveStatic('static', {'index': 'index.html'}));

            const resolver = cert
                ? () => {
                    if (this.httpServer.listening && this.httpsServer.listening) {
                        resolve({httpPort: this.httpPort, httpsPort: this.httpsPort});
                    }
                }
                : () => resolve({httpPort: this.httpPort});

            this.httpServer = require('http').createServer(app).listen(this.httpPort);
            this.httpServer.once('listening', () => {
                console.error(`Static server started on http://localhost:${this.httpPort}`);
                resolver();
            });
            this.httpServer.on('error', (error) => {
                if (this.httpServer.listening) {
                    // ошибка при запущенном сервере, запускаем деактивацию
                    done(error);
                } else {
                    // ошибка при запуске сервера, reject останавливает активацию и вызывает деактивацию
                    reject(error);
                }
            });

            if (cert) {
                const opts = createHttpsOpts(cert);
                this.httpsServer = require('https').createServer(opts, app).listen(this.httpsPort);
                this.httpsServer.once('listening', () => {
                    console.error(`Static server started on https://localhost:${this.httpsPort}`);
                    resolver();
                });
                this.httpsServer.on('error', (error) => {
                    if (this.httpsServer.listening) {
                        // ошибка при запущенном сервере, запускаем деактивацию
                        done(error);
                    } else {
                        // ошибка при запуске сервера, reject останавливает активацию и вызывает деактивацию
                        reject(error);
                    }
                });
            }
        });
    }

    async shutdown() {
        await Promise.all([
            new Promise((resolve) => {
                if (this.httpServer) {
                    this.httpServer.close(resolve);
                } else {
                    resolve();
                }
            }),
            new Promise((resolve) => {
                if (this.httpsServer) {
                    this.httpsServer.close(resolve);
                } else {
                    resolve();
                }
            })
        ]);
    }
};
```

Поскольку теперь мы отдаем статику по обоим протоколам, нам нужно два сервера, и резолв Promise `init` должен
происходить после того, как оба сервера будут готовы к работе. Также для создания сервера, отвечающего по HTTPS, нужно
настроить сертификаты, и как раз для этого используются результаты активации компонента `cert` (которые достаются из
`results`). Чтобы их получить, нужно проставить его в зависимости компонета сервера, и это делается в конструкторе
компонента установкой свойства `deps`. 

Теперь нужно из этих двух компонентов собрать команду. Команда будет иметь описание и две опции для задания портов. Создаем файл [`static-server-https.js`](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-example/configs/archon/commands/static-server-https.js):

```js
'use strict';

const StaticServer = require('../components/static-server-https');
const cert = require('@yandex-int/internal-cert').components;

module.exports = {
    name: 'serve-static-https',
    description: 'Start static server',
    setup(command) {
        return command
            .options({
                'http-port': {
                    alias: 'p',
                    type: 'number',
                    description: 'HTTP port',
                    requiresArg: true,
                    default: 3333
                },
                'https-port': {
                    alias: 's',
                    type: 'number',
                    description: 'HTTPS port',
                    requiresArg: true,
                    default: 3443
                }
            });
    },
    graph(options) {
        return [
            cert.generate({
                name: 'cert-gen'
            }),
            new StaticServer({
                name: 'server',
                deps: ['cert-gen'],
                transformInput(results) {
                    return {
                        cert: results.get('cert-gen')
                    };
                },
                httpPort: options.httpPort,
                httpsPort: options.httpsPort
            })
        ];
    }
};
```

Получилась команда `serve-static-https` с опциями для задания портов и графом компонент из двух элементов, причём
`cert` не имеет зависимостей, а `server` зависит от `cert` (и получит результаты его инициализации).

Пришло время добавить команду в конфигурацию [Archon]. Также вместе с ней добавим команду из модуля `@yandex-int/internal-cert`:
```json
{
    "commands": [
        "@yandex-int/internal-cert/commands/cert",
        "./commands/static-server-https"
    ]
}
```
Теперь можно запустить сервер. При первом запуске будут сгенерированы сертификаты и при последующих генерация будет
пропущена:

```
$ archon serve-static-https
Генерируем сертификаты
Добавляем сертификаты в KeyChain
Static server started on http://localhost:3333
Static server started on https://localhost:3443
```

И по адресам http://localhost:3333 и https://localhost:3443 можно увидеть [статическую страницу с котиком](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-example/static/index.html).

Также можно запустить генерацию или очистку сертификатов при помощи команды из модуля `@yandex-int/internal-cert`:

```
$ archon cert
Генерируем сертификаты
Добавляем сертификаты в KeyChain
```

```
$ archon cert --clean
Сертификаты удалены из KeyChain
```

# Заключение

Больше подробностей про создание команд и компонентов можно прочитать в документации [Archon] в разделе
[Создание команд и компонентов](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon.html#sozdanie-komand-i-komponentov).


[Archon]: https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon.html
