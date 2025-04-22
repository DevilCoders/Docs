# Travel Crowdtest Proxy Service

Сервис позволяет внешним асессорам, заходить по [webAuth](https://wiki.yandex-team.ru/intranet/webauth/)
и тестировать приложения в тестовых окружениях [группы разработки фронтенда Яндекс Путешествий](https://abc.yandex-team.ru/services/portalvteam/?scope=development).

## Описание работы

Балансировщик `travel-frontend-crowdtest-balancer` предоставляет авторизацию, проверку доступов и в случае успеха отправляет к crowdtest.
Crowdtest проксирует через себя запросы до приложений при этом задает необходимые маркирующие заголовки.
Конфигурация nginx находится в директории `./deploy/nginx/`.

## Стенды

Сервис также позволяет внешним асессорами тестировать стенды на ферме Путешествий или стендах на PR Расписаний.
При переходе по специальному пути на `crowdtest`, в котором содержится идентификатор стенда, идентификатор сохраняется в куках
и происходит редирект на `/`, который уже проксирует на определенный в куке стенд.

## Выкатка

1. Проект в [Deploy](https://deploy.yandex-team.ru/projects/travel-frontend-crowdtest-proxy).
2. Балансер в [Awacs](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-crowdtest-balancer/).
3. Автоматический релиз на пуш в `trunk` через CI

## Сетевые доступы в Puncher

1. Для доступа от балансера `travel-frontend-crowdtest-balancer` до приложения `travel-frontend-crowdtest-proxy` заказаны доступы: `_CROWDTEST_BALANCER_NETS_` -> `_YA_TRAVEL_CROWDTEST_NETS_`. [link](https://puncher.yandex-team.ru/?id=5e60183ea357db84263cae62)
2. Для доступа от приложения `travel-frontend-crowdtest-proxy` до балансера `travel-test` заказаны доступы: `_YA_TRAVEL_CROWDTEST_NETS_` -> `travel-frontend-testing-balancer-l3.yandex-team.ru`. [link](https://puncher.yandex-team.ru/?id=6130766d17994dccabc0a903)
3. Для доступа разработчкам до приложения `travel-crowdtest-proxy `заказаны доступы: `Разработка (Фронтенд Яндекс.Путешествий)` -> `_YA_TRAVEL_CROWDTEST_NETS_`. Порты [22](https://puncher.yandex-team.ru/?id=5e5fa768c57f77f3c808f3fa), [80,443](https://puncher.yandex-team.ru/?id=6141bb837ab0652c8c277069)
4. Для доступа до стендов заказаны доступы от сети приложения `travel-frontend-crowdtest-proxy` до сети стендов: `_YA_TRAVEL_CROWDTEST_NETS_` -> `_DATAUI_TRAVEL_NETS_` [link](https://puncher.yandex-team.ru/?id=5e71284e1fe4f3a5f407abcf)

## Сервисы

### travel-frontend-portal

Яндекс Путешествия

#### testing

Тестинг Яндекс Путешествий

Адрес в crowdtest `https://travel.crowdtest.yandex.ru/`
проксируется в `https://travel-test.yandex.ru/`

#### farm

Ферма со стендами на PR

Адрес в crowdtest `https://travel-farm.crowdtest.yandex.ru/farmId/{farmId}`
проксируется в `https://portal_{farmId}.travel.farm.yandex.ru/`,

где `{farmId}` - это имя ветки с замененной `/` на `_`, например `users_isaven_travelfront-7945`.

### travel-frontend-rasp

Яндекс Расписания

#### testing

Тестинг Яндекс Расписаний

Адрес в crowdtest `https://{device_prefix}.rasp.crowdtest.yandex.{tld}/`
проксируется в `https://{device_prefix}.testing.morda-front.rasp.common.yandex.{tld}`,

где `{device_prefix}` - это `t` или ` ` тип устройства тач/десктоп,
`{tld}` - национальный домен `ru`, `ua`, `kz`, `uz`, `by`, `com`, `net`.

#### stand

Стенды запускаемые на PR

Адрес в crowdtest `https://{device_prefix}.rasp-stand.crowdtest.yandex.{tld}/prId/{prId}`
проксируется в `https://pr-{prId}.unstable.{device_prefix}.rasp.common.yandex.ru/`,

где `{prId}` - это номер PR, например `2588799`, `{device_prefix}` - это `t` или ` ` тип устройства тач/десктоп,
`{tld}` - национальный домен `ru`, `ua`, `kz`, `uz`, `by`, `com`, `net`.
