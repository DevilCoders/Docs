# luster-bunker

```
npm install --registry=https://npm.yandex-team.ru @vertis/luster-bunker
```

Плагин `luster` для работы с бункером. Мастер-процесс загружает и периодически обновляет данные бункера и рассылает их воркерам.

Для того, чтобы избежать возможности падения сервиса на старте из-за недоступности бункера, в плагине реализована возможность загружать предкешированные данные из файла.
В продакшене **настоятельно рекомендуется** использовать эту возможность.

В отличие от v2, где кеш предоставлял отдельный крон [vertis-bunker-cache](https://github.com/YandexClassifieds/vertis-bunker-cache) и в интересах контейниризации, плагин умеет делать кеш сам.

**Схема работы:**

В `development` не используем кеш, а выкачиваем данные из бункера. 

При сборке пакета/контейнера создаем кеш `npx luster-bunker-cache configs/production/luster.js path/to/cache.json`,
приложение стартует с этим кешом и в фоне подтягивает актуальные данные из бункера.

## Подключение и настройка

`luster.conf.js`

```javascript
{
    extensions: {
        'luster-buner': {
            // интервал обновления в ms (по умолчанию, 10 минут)
            refresh: 10 * 60000,
            // путь до кеша, созданного luster-bunker-precache
            'cachePath': 'path/to/cache.json',
            // опции для запроса http-бункера (отправляются в asker как есть)
            connection: {
                family: 6,
                host: 'bunker-api.yandex.net',
                timeout: 500,
                maxRetries: 10,
                requestId: 'luster-bunker',
            },
            // массив нод, которые надо рекурсивно загрузить
            nodes: [
                {
                    node: '/auto_ru',
                    version: 'stable',
                },
                {
                    node: '/vertis-moderation/autoru',
                    version: 'stable',
                },
            ],
        }
    }
}
```

## Usage

```javascript
const bunker = require('luster').bunker;
const nodesData = bunker.configureAPI();

const bunkerNodeData = nodesData.getNode('/auto_ru/ads/test');
```

## API

```javascript
const bunker = require('luster').bunker;
```

#### `bunker.configureAPI(): Object`

```javascript
const nodesData = bunker.configureAPI();
```

#### `nodesData.getNode(path: String): *`

```javascript
const bunkerNodeData = nodesData.getNode('/auto_ru/ads/test');
```

## development

Посмотреть как локально работает скачивание бункера можно на примере
```
node ./bin/luster-bunker-cache.js examples/luster-config.js examples/bunker-cache.json
```
