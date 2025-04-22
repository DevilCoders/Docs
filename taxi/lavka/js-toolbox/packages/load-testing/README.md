# load-testing

## Схема работы

-   Модуль перехватывает все http запросы и кэширует их в памяти
-   Если кэш запроса уже есть в памяти, то ответ берется из кэша (реальный http запрос не отправляется)
-   Кэш из памяти интервально сохраняется на жесткий диск
-   Если указаны AWS параметры, то кэш также сохраняется в AWS
-   При старте приложения кеш загружается из AWS (если используется)

## Опции

```ts
export type LoadTestingOptions = {
    logLevel: 'DEBUG' | 'INFO' | 'ERROR';
    logsFile: string; // путь к лог файлу (если не указан, то логи не пишутся)
    artifactsDir: string; // путь к папке с артефактами
    recordingName: string; // название авто-тестов
    headFile: string; // имя заглавного файла кэша (`index.json` по умолчанию)
    persistInterval: number; // seconds: кэш сохраняется через указанный интервал
    polly: {
        logging: boolean;
    };
    awsClient: {
        enabled: boolean;
        host: string;
        bucket: string;
        key: string;
        secret: string;
        prefix: string;
    };
};
```

## Express provider

```ts
import express from 'express';
import {initLoadTesting, isLoadTestingEnabled, loadTesting} from '@lavka-js-toolbox/load-testing';

async function start() {
    await initLoadTesting(process.env.LOAD_TESTING === '1', {
        /* LoadTestingOptions */
    });

    const app = express();

    if (isLoadTestingEnabled(loadTesting)) {
        loadTesting.api.createExpressProvider(app);

        loadTesting.api.express().setModifyHeadersHook((headers) => {
            if (headers['x-idempotency-token']) {
                // фиксируем токен идемпотентности
                headers['x-idempotency-token'] = '4q1TXqo_h3wCwm5-TXJEj';
            }

            return headers;
        });
    }
}
```

-   `setModifyHeadersHook` — хук для перехвата заголовков запросов
    (см. [также](https://netflix.github.io/pollyjs/#/configuration?id=headers))

-   `setModifyBodyHook` — хук для перехвата тела запросов
    (см. [также](https://netflix.github.io/pollyjs/#/configuration?id=body))
