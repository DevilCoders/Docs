# API-Сервис для автоматизации ручного тестирования

## Разработка

Устанавливаем зависимости:
```bash
npx lerna bootstrap --scope @yandex-int/crowdtest-runner --include-filtered-dependencies
```

Для локальной разработки запускаем скрипт:
```bash
npx lerna run dev --scope @yandex-int/crowdtest-runner --stream
```

API становится доступно по адресу [http://localhost:8080](http://localhost:8080).
Приложение автоматически перезапустится при изменениях в коде.

Для работы нужны `TESTPALM_OAUTH_TOKEN`, `SANDBOX_OAUTH_TOKEN` и `BOOKING_OAUTH_TOKEN`. 
Для избежания ошибки "500 Internal Server Error - self signed certificate in certificate chain" требуется задать опцию `NODE_TLS_REJECT_UNAUTHORIZED='0'`.

Для того, чтобы использовать тестовый контур [Брониратора](https://booking.yandex-team.ru/#/help?section=api) - следует задать опцию `BOOKING_BASE_URL=https://sandbox.booking.yandex-team.ru/api`.