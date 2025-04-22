# release-tag-search

Нужно для правильного запуска Pulse тасок, которому нужно передать два коммита - текущий и `base`.
В релизах `base` является HEAD коммит предыдущего релиза.

Утилита позволяет искать `base` относительно текущего релиза.

## Установка

```console
npm i @yandex-int/previous-release --registry=https://npm.yandex-team.ru
```

## Требования

### ARC_TOKEN
В переменной окружения `ARC_TOKEN` должен быть указан OAuth-токен пользователя, от имени которого будет выполняться запросы к Arc.
Узнать свой токен можно по [ссылке][get-arc-oauth-token].

### NODE_EXTRA_CA_CERTS
В переменной окружения `NODE_EXTRA_CA_CERTS` должен быть указан путь к сертификату `YandexInternalRootCA.crt`. Сертификат можно скачать по [ссылке][get-cert].

### Сетевые доступы ("дырки")
Для работы пакета нужен доступ к `api.arc-vcs.yandex-team.ru:6734` (gRPC API арка). Оставить заявку в Puncher можно по [ссылке][arc_api_access].

[get-cert]: https://crls.yandex.net/YandexInternalRootCA.crt
[get-arc-oauth-token]: https://nda.ya.ru/t/qPiF_BwS3WKLuC
[arc_api_access]: https://puncher.yandex-team.ru?create_destinations=api.arc-vcs.yandex-team.ru&create_protocol=tcp&create_locations=office&create_locations=vpn&create_ports=6734

## Использование
```typescript
import { searchPreviousReleaseTagRelativeToRef, fetchLatestTagByNamespace } from "@yandex-int/release-tag-search";

const tag = await searchPreviousReleaseTagRelativeToRef("releases/frontend/web4/v1.1115.0");

// {
//   "version": "v1.1114.0",
//   "namespace": "tags/releases/frontend/web4",
//   "name": "tags/releases/frontend/web4/v1.1114.0",
//   "hash": "ef28323aa726928c264e9262a1265cbe0bab781e",
//   "treeHash": "a3a3a610fb399771affc34b3c64ec67dc8fc151d"
// }

const currentTag = await fetchLatestTagByNamespace("tags/releases/frontend/web4/");
// {
//   version: 'v1.1199.0',
//   namespace: 'tags/releases/frontend/web4',
//   name: 'tags/releases/frontend/web4/v1.1199.0',
//   hash: 'ade146ae32db0334adf67cc31807ce02df69f53b',
//   treeHash: '562291de2b16b52af78f1c95e2d9aac2d314a0ca'
}
```

```console
export ARC_TOKEN="<TOKEN>"
export NODE_EXTRA_CA_CERTS="<CERT-PATH>"

npx "@yandex-int/release-tag-search previous --ref releases/frontend/web4/v1.1115.0 | jq "."

// {
//   "version": "v1.1114.0",
//   "namespace": "tags/releases/frontend/web4",
//   "name": "tags/releases/frontend/web4/v1.1114.0",
//   "hash": "ef28323aa726928c264e9262a1265cbe0bab781e",
//   "treeHash": "a3a3a610fb399771affc34b3c64ec67dc8fc151d"
// }
```
