# Выводит отвественных для переданного хоста

Поддерживает хосты из голема, gencfg и qloud.

## Использование
 Определить переменную окружения `OAUTH_TOKEN` для доступа к gencfg и qloud. Можно взять значение из `QTOOLS_TOKEN`.

```
$ ./get_responsibles.sh iva1-578e103dd0f5.qloud-c.yandex.net
[QLOUD]
https://staff.yandex-team.ru/dbrylev
https://staff.yandex-team.ru/yashunsky
https://staff.yandex-team.ru/tolmalev

$ ./get_responsibles.sh iva1-5523-739-iva-market-prod--41c-18226.gencfg-c.yandex.net
[GENCFG]
https://staff.yandex-team.ru/yandex_monetize_market_marketdev_admin
https://staff.yandex-team.ru/d3rp
https://staff.yandex-team.ru/le087
https://staff.yandex-team.ru/strkate
https://staff.yandex-team.ru/maxk
https://staff.yandex-team.ru/slyder
https://staff.yandex-team.ru/idonin
https://staff.yandex-team.ru/dukeartem
https://staff.yandex-team.ru/adubrovin
https://staff.yandex-team.ru/kemsta
https://staff.yandex-team.ru/asimakov

$ ./get_responsibles.sh acamar.maps.dev.yandex.net
[GOLEM]
https://staff.yandex-team.ru/ponomarev
https://staff.yandex-team.ru/martikainen
https://staff.yandex-team.ru/khrolenko
https://staff.yandex-team.ru/ykirpichev
https://staff.yandex-team.ru/thegeorg
https://staff.yandex-team.ru/tervlad
https://staff.yandex-team.ru/vmazaev
https://staff.yandex-team.ru/morbid
```
