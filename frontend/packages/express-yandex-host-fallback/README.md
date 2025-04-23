# express-yandex-host-fallback

[![Build Status](https://drone.yandex-team.ru/api/badges/project-stub/express-yandex-host-fallback/status.svg)](https://drone.yandex-team.ru/project-stub/express-yandex-host-fallback)

В случае, если отсутствует req.headers.host, запишет его из options. Это необходимо для работы
мидлвар, которые полагаются на host (например, вытаскивают из него TLD). Ситуация, когда
host отсутствует может произойти, например, при включенном
[healthcheck компонента](https://docs.platform.yandex-team.ru/doc/healthcheck/healthcheck) в кулауде.

## Установка

```bash
npm install express-yandex-host-fallback -S
```

## Подключение
```js
const app = require('express')();
app.use(require('express-yandex-host-fallback')({ host: 'yandex.ru' }));
```