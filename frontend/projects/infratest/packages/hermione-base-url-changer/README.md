# hermione-base-url-changer

Плагин для hermione, который меняет [baseUrl](https://github.com/gemini-testing/hermione#baseurl).
Работает в паре с командой [@yandex-int/archon-hermione](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/archon-hermione).
А точнее общается с компонентом из её графа [@yandex-int/archon-tunneler](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/archon-tunneler)
по ipbus: на старте прогона hermione и при переподнятии туннеля плагин получает актуальный публичный url.

## Использование

Если вы настраиваете свою команду для поднятия гермионы и туннелера, вам нужно передать в гермиону и в туннелер одинаковые настройки ipbus.

Пример команды в сервисе, которая поднимает приложение, туннелер и гермиону:

```javascript
// .config/archon/commands/hermione.js

const { MyApp } = require('../components/my-app');

const { Hermione } = require('@yandex-int/archon-hermione').components;
const { Tunneler } = require('@yandex-int/archon-tunneler').components;
const { generateBrokerRunDir, generateBrokerLogDir } = require('@yandex-int/ipbus');

const description = 'Команда arсhon для запуска hermione';

module.exports = {
    name: 'hermione',
    description,
    setup(command) {
        return command
            .usage(description);
    },

    async graph(options) {
        const appPort = await getPort();

        // Генерируем пути для ipbus
        const ipbusBrokerRunDir = generateBrokerRunDir();
        const ipbusBrokerLogDir = generateBrokerLogDir();

        const graph = [];

        graph.push(
            new MyApp({
                name: 'myapp',
                options: {
                    port: appPort,
                }
            }),
            new Tunneler({
                name: 'tunneler',
                options: {
                    domains: ['yandex.ru'],
                    port: appPort,
                    silent: true,
                    // с опцией watcher: true туннелер будет писать в ipbus адрес поднятого туннеля
                    watcher: true,
                    // сообщим ему, в какой именно топик
                    ipbusBrokerRunDir,
                    ipbusBrokerLogDir,
                },
                deps: ['myapp'],
            }),
            new Hermione({
                options: {
                    // в гермиону нужно передать путь к ipbus, который мы передали в tunneler
                    ipbusBrokerRunDir,
                    ipbusBrokerLogDir,
                },
                deps: ['tunneler'],
            }),
        );

        return graph;
    }
};
```

После этого достаточно включить плагин в конфиге гермионы:

```javascript
// .hermione.conf.js

module.exports = {
    plugins: {
        "@yandex-int/hermione-base-url-changer": {
            enabled: true
        }
    }
};
```
