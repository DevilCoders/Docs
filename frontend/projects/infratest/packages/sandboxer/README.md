# Sandboxer

> Удобный клиент для работы с [Sandbox REST API](https://sandbox.yandex-team.ru/media/swagger-ui/). Обёртка над [sandbox-client](https://github.yandex-team.ru/sandbox-ci/sandbox-client)

## Установка

```shell
npm i @yandex-int/sandboxer --registry http://npm.yandex-team.ru
```

## Использование

```js
const Sandboxer = require('@yandex-int/sandboxer');

const sandbox = new Sandboxer({
    token: 'dummy',
    retry: {
        retries: 10,
        factor: 1.5,
        minTimeout: 2500,
        maxTimeout: 15000
    }
});

sandbox.task.load(1234).then(console.log);

sandbox.task.start({ type: 'some_type', owner: 'some_owner' }).then(console.log);

sandbox.resource.finder.find({ limit: 4, offset: 10 }).then(console.log);
```

## Документация

Полная документация сгенерирована на основе исходного кода и доступна на [GitHub Pages в этом репозитории](https://github.yandex-team.ru/pages/sandbox-ci/sandboxer/index.html).

## FAQ

### Почему просто не использовать `sandbox-client`?

Пакет [sandbox-client](https://github.yandex-team.ru/sandbox-ci/sandbox-client) генерируется при помощи [Swagger Codegen](https://github.com/swagger-api/swagger-codegen) на основе [swager.json](https://sandbox.yandex-team.ru/api/v1.0/swagger.json).

Это означает, что API модуля полностью повторяет REST API самого SandBox, которое не всегда удобно. Например, чтобы запустить задачу нужно выполнить 2 HTTP запроса.

Пакет `sandbox-client` можно использовать для тех случаев, которые ещё не покрыты в `sandboxer`.

### Почему TypeScript?

Подробно об этом можно прочитать в [FEI-6647](https://st.yandex-team.ru/FEI-6647).

## Похожее

* [yasandbox](https://github.yandex-team.ru/search-interfaces/yasandbox)
* [sandbox-client](https://github.yandex-team.ru/sandbox-ci/sandbox-client)
* [sandbox-client-dynamic](https://github.yandex-team.ru/sandbox-ci/sandbox-client-dynamic)
* [sandbox-client-2](https://github.yandex-team.ru/sandbox-ci/sandbox-client-2)
* [sandbox-yaml-to-swagger](https://github.yandex-team.ru/sandbox-ci/sandbox-yaml-to-swagger)

## Разработка

* `npm test` — Запуск unit-тестов (требует предварительной компиляции).
* `npm lint` — Запуск линтера.
* `npm run build` – Полная сборка проекта.
* `npm run watch` – Запуск автоматической пересборки проекта при изменении файлов.
* `npm run deploy` – Сборка и деплой документации, используя [typedoc](https://github.com/TypeStrong/typedoc).
* `npm run clean` - Очистка сгенерированных файлов.
