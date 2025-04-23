# Плагин для запуска clement при прогоне hermione тестов

Плагин позволяет записать дампы HTTP запросов с помощью [clement](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/clement), а затем использовать их для повторного запуска тестов.


## Подключение на проекте

Установить пакет в проект:
```bash
npm install --save-dev @yandex-int/hermione-clement
```

Настроить плагин в `hermione.conf.js`. Пример:
```js
const hermioneConfig = {
    '@yandex-int/hermione-clement': {
        enabled: true,
        logLevel: 'info',
        config: {
            sources: { 
                // Порт, на котором будет слушать clement и проксировать запросы на https://yandex.ru
                3333: {
                    url: 'https://yandex.ru',

                    // Конфигурационные секции, позволяющие переопределить параметры проксирования
                    // и набор плагинов на основе сопоставления с запросом (функции-матчера).
                    configs: [
                        {
                            // Матчер по умолчанию сопоставляет `cfg.path` (массив строк или регулярных выражений) с `req.parsedURL.pathname`.
                            // matcher: (cfg, req) => true,
    
                            // Путь URL, для которого будет применен конфиг.
                            path: /.*/,
    
                            // Переходить по редиректам (или нет) при проксировании.
                            // Параметр передается в запрос за ответом бэкэнда, который мы делаем при помощи got (https://github.com/sindresorhus/got#followredirect).
                            followRedirect: true,
    
                            // Плагины выполняются перед плагинами самого clement.
                            plugins: [
                                require('./plugins/cache-key')
                            ],
          
                            // Где хранить дампы (по умолчанию – .config/clement/cache).
                            cachePath: path.resolve(__dirname, '..', 'dumps'),
          
                            // Переопределение параметров запроса:
                            // protocol, host, port, method, path, query, headers, body
                            source: {
                                headers: { 'x-foo': 42 },
                                query: { foo: 'bar' }
                            }
                        }
                    ]
                },
            // ...
            }  
        },
    },  
};
```

Подробнее про конфигурацию написано в документации к [clement](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/clement).

## Параметры запуска тестов

По умолчанию clement просто проксирует через себя HTTP запросы, ничего не сохраняя на диск. Параметры запуска hermione:

- `--save` – запись новых дампов на диск.
- `--play` – воспроизведение ранее записанных дампов. Если дамп для какого-либо запрос не найден, то будет ошибка.
- `--create` – воспроизведение ранее записанных дампов. Если дамп для какого-либо запрос не найден, то он будет создан.
