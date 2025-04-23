# Private Arcanum API Node.js Client

Node.js клиент для работы с [приватным Arcanum API][private_arcanum_api].

> :warning: Используйте на свой страх и риск. Команда Arcanum оставляет за собой право вносить обратнонесовместимые изменения.
> 
> Однако [публичный API][public_arcanum_api] пока ещё очень скудный и покрывает лишь небольшое количество задач по работе с Arcanum.

[private_arcanum_api]: https://a.yandex-team.ru/api/swagger/index.html?url=https%3A%2F%2Fa.yandex-team.ru%2Fapi%2Fswagger.json
[public_arcanum_api]: https://a.yandex-team.ru/api/swagger/index.html

## Использование

```ts
import { configureApiController, ArcanumApiEndpoint, generated } from "@yandex-int/si.ci.arcanum-api";

const endpoint = ArcanumApiEndpoint.Testing;
const token = 'my-secret';

(async () => {
    const arcanumVcsClient = configureApiController(generated.VcsApi, endpoint, token);

    const limit = undefined;
    const pattern = "junk";
    const fields = "name";

    const branches = await arcanumVcsClient.getBranches('ARC', pattern, limit, fields);

    console.log(branches.body.data);
})();
```

> В примере, `VcsApi` автосгенерированный класс для работы с [vcs](https://a.yandex-team.ru/api/swagger/index.html#/vcs).

## API

### Настройки

#### endpoint

Url к Arcanum API.

Возможные значения:

* `https://a.yandex-team.ru/api` (production)
* `https://appserver-arcanum2.n.yandex-team.ru/api` (testing)

По умолчанию — [https://a.yandex-team.ru/api](https://a.yandex-team.ru/api).

#### token

OAuth token для работы с Arcanum API. По умолчанию значение будет взято из переменной окружения `ARCANUM_API_OAUTH_TOKEN`.

> Для получения OAuth-токена зайдите из под нужного пользователя по ссылке: https://a.yandex-team.ru/api/token. Получите значение из поля `access_token`.

### Переменные окружения

* `ARCANUM_API_ENDPOINT` — URL к Arcanum API. 
* `ARCANUM_API_OAUTH_TOKEN` — OAuth-токен для работы с Arcanum API.

### Классы для работы с API

Полный список сгенерированных классов доступен в директории [generated](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/arcanum-api/src/generated/api/apis.ts).

В сгенерированных классах не настроена авторизация. Для работы используйте обёртку `configureApiController(<GeneratedArcanumApiGroupConstructor>)`.

## Разработка

### Структура кода

* `src/generated` — сгенерированный код на основе [swagger.json][swagger_json].
* `src/lib` — дополнительные код библиотеки, написанный вручную. Экспортируется и является публичным API npm-пакета.
* `src/util` — хэлперы для работы библиотеки. Не экспортируются и не являются публичным API npm-пакета.

### Автогенерация клиента к API на основе swagger.json

Если в Arcanum API что-то изменилось, нужно перегенерировать директорию `generated` с помощью [openapi-generator](https://openapi-generator.tech/) на основе [swagger.json][swagger_json].

[swagger_json]: https://a.yandex-team.ru/api/swagger.json

```shell
npm run generate
```

И затем заменить `Bearer` на `OAuth` в `src/generated/model/models.ts` (класс `OAuth` метод `applyToRequest`). Подробнее в https://st.yandex-team.ru/DEVTOOLSSUPPORT-14360

> Подробнее о настройках для `typescript-node` читайте в [документации](https://openapi-generator.tech/docs/generators/typescript-node).

Ошибки линтеров исправлять не нужно, директория `generated` добавлена в `.eslintignore`.
