# Contributing

## Как разрабатывать

Требования:

* nodejs >= 12.11.1
* [docker](https://docs.docker.com/docker-for-mac/)

Если вы только начинаете знакомство с docker, qloud и всем что вокруг этого, почитайте [руководство Вадима Макишвили](https://gitlab.yandex-team.ru/makishvili/about).

```bash
npm ci
npm run dev # localhost:8080
# or
PORT=8888 npm run dev # localhost:8888
```

### OAuth токены

В проекте используются [секреты](https://yav.yandex-team.ru/secret/sec-01cjz1hw16ymy62e9f917k8gdk) (и специальные [testing-секреты](https://yav.yandex-team.ru/secret/sec-01cjz1zmeqzc10c3kjr0vjrdw5) для моков). Для запуска локально нужно поместить необходимые токены в переменные окружения (детали можно прочитать в `.env_stub`).

Удобнее всего для этого скопировать `.env_stub` в корне проекта в `.env` и указать требуемые токены из секретницы.

### Как собрать образ

```bash
npx qtools build
```

### Как проверить образ локально

```bash
docker images # найти <IMAGE_ID>
docker run -itp 127.0.0.1:3000:80 <IMAGE_ID> # localhost:3000
```

## Как выкладывать

1. Вмержить новую функциональность в `trunk`.
2. При пуше нового коммита автоматически соберётся [`testing`](https://deploy.yandex-team.ru/stages/maps-front-podrick-int_testing)
3. Дождаться выкладки тестинга и проверить его работоспособность, например, дёрнув ручку пинг.
4. Покатить дополнительные окружения
- Если изменяли файлы в `server/projects/mocks`, нужно вручную обновить окружения
[mocks](https://deploy.yandex-team.ru/stages/maps-front-podrick-int_mocks) и
[stress](https://deploy.yandex-team.ru/stages/maps-front-podrick-int_stress)
    ```bash
    npx qtools deploy mocks
    npx qtools deploy stress
    ```
- Если изменяли файлы в `server/projects/static`, нужно вручную обновить окружение
[static](https://deploy.yandex-team.ru/stages/maps-front-podrick-int_static)
    ```bash
    npx qtools deploy static
    ```
- Если изменения в других проектах, нужно обновить [common](https://deploy.yandex-team.ru/stages/maps-front-podrick-int_common) — основное окружение с приложением
    ```bash
    npx qtools deploy common
    ```

При необходимости в последнем шаге добавьте `--force`, если изменения в конфиге деплоя корректные.

> Не забудь для себя [получить токен](https://a.yandex-team.ru/arcadia/maps/front/packages/qtools#authorization).

## Критичные сервисы

В podrick-int есть критичные проекты, которые не должны ломаться при изменении остальных проектов, например `mocks` или `static`. Для них заведены отдельные окружения.

Разработчики этих проектов сами следят за ними и выкладывают только при полной уверенности в работоспособности.

## Code quality

* [mocha](http://mochajs.org/) for tests
* [nyc](https://istanbul.js.org/) for code coverage
