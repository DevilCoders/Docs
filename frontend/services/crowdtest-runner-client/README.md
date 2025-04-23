# Клиент для сервиса [crowdtest-runner](../crowdtest-runner)

## Разработка

Устанавливаем зависимости:
```bash
npx lerna bootstrap --scope @yandex-int/crowdtest-runner-client --include-filtered-dependencies
```

Для сборки в production-режиме запускаем:
```bash
npx lerna run build --scope @yandex-int/crowdtest-runner-client
```

### Локальная разработка

Для локальной разработки запускаем скрипт:
```bash
npx lerna run dev --scope @yandex-int/crowdtest-runner-client --stream
```

Также для локальной разработки потребуется запущенный сервис [crowdtest-runner](../crowdtest-runner).
Для избежания ошибки "500 Internal Server Error - self signed certificate in certificate chain" требуется задать опцию `NODE_TLS_REJECT_UNAUTHORIZED='0'`.

В проекте используется опция `BOOKING_BASE_URL`, которая определяет адрес, на который будут отправляться запросы к [Брониратору](https://booking.yandex-team.ru/#/help?section=api-calendar). Значение по умолчанию: `https://booking.yandex-team.ru`. Таким образом при локальной разработке и тестировании - следует явно указать опцию `BOOKING_BASE_URL=https://sandbox.booking.yandex-team.ru/api`.

Единая команда локального запуска:
```bash
BOOKING_BASE_URL=https://sandbox.booking.yandex-team.ru/api NODE_TLS_REJECT_UNAUTHORIZED='0' npx lerna run dev --scope @yandex-int/crowdtest-runner --scope @yandex-int/crowdtest-runner-client --stream
```

При первом запуске база данных будет пустой. Чтобы добавить в нее данных для тестирования, нужно собрать [payload](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/crowdtest-runner/test/create-launch-from-testpalm.test.ts?rev=r6883552#L49-55) и отправить его на локальный api
Пример запроса:
```bash
curl -X POST -H 'Content-Type: application/x-www-form-urlencoded' http://localhost:8080/api/v1/launch/create-from-testpalm -d 'title=test-title&type=testsuite&project=serp-js&author=robot-serp-bot&content=%7B%22testSuiteId%22%3A%225f58e4c28807112718f1fc43%22%2C%22expression%22%3A%22%7B%7D%22%7D'
```



Сервис становится доступен по адресу [http://localhost:8080](http://localhost:8080).
Работает Hot Module Replacement, изменения в клиентском коде будут происходить автоматически на лету.
