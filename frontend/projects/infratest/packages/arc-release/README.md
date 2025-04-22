# arc-release

## Установка

```console
npm i @yandex-int/arc-release --registry=https://npm.yandex-team.ru
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
