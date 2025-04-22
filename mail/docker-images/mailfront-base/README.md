# `mailfront-base` image

Универсальный образ для Qloud и Deploy для фронтендов персональных сервисов.

Собирается для обратной совместимости. Рекомендуется переезжать на связку
общего образа `mail-base-focal:rNNN` + ресурс.

## Changelog

https://wiki.yandex-team.ru/pochta/sre/deploy/front/#changelog

## How to use

https://wiki.yandex-team.ru/pochta/sre/deploy/front/


## How to build

### CI

Сборка запускается в CI на каждый PR, пушит в registry с тегом `pr-XXX-N` (`XXX` — номер PR, `N` — номер сборки).

Сборка с пушем тега `rNNN` (`NNN` — номер ревизии) запускается на каждый merge в trunk.

Сборка автоматически запускается при попавших в trunk изменениях [mail-base](../mail-base)

### local

Just run `make` to test the build. It will build `tmp` tag
and will **not push** it to registry.

Run `make tag=TAG` to build and **push** other tags.
```
make tag=prestable
```

Production release tag is `rNNN`.

There are aliases targets for common tags:
`make unstable`, `make prestable` and `make unified`.
