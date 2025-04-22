# Клиент для работы с Warden API

[Документация по Warden API](https://wiki.yandex-team.ru/jandekspoisk/sepe/dezhurnajasmena/warden/api/)

## Установка

```bash
npm install @yandex-int/warden-api-client
```

## Использование

```ts
import { createClient } from "@yandex-int/warden-api-client";

(async () => {
    // Токен можно получить по адресу https://oauth.yandex-team.ru/authorize?response_type=token&client_id=a3891d91bf9a4afeb1b7fba8e0735d49
    const client = createClient("your token here");
    console.log(await client.getComponent({name: "report_renderer"}));
})()
    .catch(e => {
        console.error(e);
        process.exit(1);
    })

/**
 * GetComponentResponse {
 *   component: Component {
 *     name: 'report_renderer',
 *     parentComponentName: '',
 *     humanReadableName: 'Report Renderer',
 *     weight: 1,
 *     functionalityList: [],
 *     horizontal: true,
 *     monitoring: ComponentMonitoring { panels: [Array] },
 *     abcServiceSlug: 'reportrenderer',
 *     description: '',
 *     syncAbc: false,
 *     incidents: [],
 *     tags: [ [ComponentTag] ],
 * ...
 * /
```

Если нужно настроить http-клиента:
```ts
import * as https from "https";
import axios from "axios";
import { warden } from "@yandex-int/warden-api-client";
import { getCert } from "@yandex-int/yandex-internal-cert";

const httpClient = axios.create({
    headers: {"Authorization": `OAuth ${token}`}, // Авторизация делается по заголовкам
    httpsAgent: new https.Agent({ca: getCert()}), // Сервисы warden используют внутренний сертификат
});

return new warden.WardenClient(httpClient, 'https://warden.z.yandex-team.ru');
```

## Разработка

Для обновления кода клиента
```bash
npm run generate-client
```
