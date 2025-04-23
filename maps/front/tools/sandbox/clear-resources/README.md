# Скрипт для очистки квоты в сендбокс

Проставляет `ttl: 1` ресурсам `TRENDBOX_CI_REPORT_RESOURCE_BETA` и `MAPS_FRONT_BUNDLE` в сендбокс группе `MAPS_FRONT`.

## How to use

```
nvm use
npm ci
echo 'SANDBOX_OAUTH_TOKEN=<your token>' > .env
FROM=<YYYY-MM-dd> TO=<YYYY-MM-dd> npm start
```

Получить токен — https://sandbox.yandex-team.ru/oauth

Результаты работы будт в файле `result.json`
