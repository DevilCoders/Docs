# Клиент для работы с Arc gRPC API

[Документация по Arc API](https://a.yandex-team.ru/arc/trunk/arcadia/arc/api/public)

## Установка

```bash
npm install @yandex-int/si.ci.arc-api-client
```

## Требования

### Авторизация по токену
Для работы клиента необходимо авторизоваться по токену. Это можно сделать двумя способами:
* в переменной окружения `ARC_TOKEN` указать OAuth-токен пользователя, от имени которого будет выполняться запросы к Arc; узнать свой токен можно по [ссылке][get-arc-oauth-token]
* передать токен при инициализации экземпляра класса `ArcApiClient`:
```js
const arcClient = new ArcApiClient({
    certificatePath: <Путь до сертификата (подробнее ниже)>,
    token: <валидный OAuth-токен пользователя>
});
```

### NODE_EXTRA_CA_CERTS
В переменной окружения `NODE_EXTRA_CA_CERTS` должен быть указан путь к сертификату `YandexInternalRootCA.crt`. Сертификат можно скачать по [ссылке][get-cert].

### Сетевые доступы ("дырки")
Для работы пакета нужен доступ к `api.arc-vcs.yandex-team.ru:6734` (gRPC API арка). Оставить заявку в Puncher можно по [ссылке][arc_api_access].

[get-cert]: https://crls.yandex.net/YandexInternalRootCA.crt
[get-arc-oauth-token]: https://nda.ya.ru/t/qPiF_BwS3WKLuC
[arc_api_access]: https://puncher.yandex-team.ru?create_destinations=api.arc-vcs.yandex-team.ru&create_protocol=tcp&create_locations=office&create_locations=vpn&create_ports=6734

## Использование

```js
import { ArcApiClient } from "@yandex-int/si.ci.arc-api-client";

const CERTIFICATE_PATH = process.env.NODE_EXTRA_CA_CERTS;

const arcClient = new ArcApiClient({
    certificatePath: CERTIFICATE_PATH
});

// Получает все ветки/теги по префиксу, возвращает массив из объектов `ListRefsResponse.Ref`.
// @see packages/arc-api-client/proto/arc/api/public/repo_pb.d.ts:727
let refs = await arcClient.branch.listRefs({
    prefixFilter: 'releases/experimental/frontend/web4/v0.0.1'
});

refs.forEach((ref) => {
    console.log('ref name', ref.getName());
    console.log('ref HEAD commit', ref.getCommit());
});

// Отводит ветку releases/experimental/frontend/web4/v0.0.1-0 из коммита cb0a013685d5w4a654b1f4044d1b94e39c4dc0035.
await arcClient.branch.setRef({
    branch: 'releases/experimental/frontend/web4/v0.0.1-0',
    commitOid: 'cb0a013685d5w4a654b1f4044d1b94e39c4dc0035'
});

// Удаляет ветку users/zumra6a/arcanum-1e5502f6-3aa2-4c68-b8ea-05ea383ea096.
await arcClient.branch.deleteRef({
    branch: 'users/zumra6a/arcanum-1e5502f6-3aa2-4c68-b8ea-05ea383ea096'
});

// Загружает информацию о ветке.
await arcClient.branch.fetchRef('releases/experimental/frontend/web4/v0.0.1');

// Проверяет права доступа к ветке
const access = await arcClient.branch.checkRefAccess({
    login: 'robot-serp-bot',
    branch: 'users/somebody/branch'
});
// access: { create: bool, fastforward: bool, forcepush: bool, pb_delete: bool }

// Коммитит файл.
import fs from "fs";

await arcClient.commit.commitFile({
    branch: "users/<login>/some/branch",
    message: "commit message text",
    path: "path/in/arcadia/file.md",
    buffer: fs.readFileSync('/some/local/file.md')
});

// Читает содержимое файла, для текстовых файлов воспользуйтесь методом readFileText.
const binaryContent = await arcClient.file.readFile({
    revision: "some-revision",
    path: "path/in/arcadia/file.png"
});
```
