# Расположение

## Сервисы
Поднят единый (это его задача, быть одной точкой входа) сервис: [production_federated2](https://nanny.yandex-team.ru/ui/#/services/catalog/production_federated2/).

## Балансеры
Настроено два независимых балансировщика:

* Сервисный балансер, секция [production-federated](https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/production-federated).
Это изначальная конфигурация, оставлена для обратной совместимости.
* [Секция в AWACS](https://nanny.yandex-team.ru/ui/#/awacs/balancers/list/nanny-lb.yandex-team.ru/).
Эта конфигурация поднята для того, чтобы не открывать доступ до "коммунального" сервисного балансера (один общий IP на все сервисы).

## Доступ
* Доступен через HTTP(S): `http://federated.n.yandex-team.ru/`
* Доступен через HTTP(S): `http://federated.yandex-team.ru/`

