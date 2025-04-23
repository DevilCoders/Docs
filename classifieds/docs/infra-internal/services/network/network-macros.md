# Сетевые макросы Вертикалей

Для удобства заказа доступов и управления сетями используются сетевые макросы. Ниже описаны соответствующие сетевые макросы в продовом и тестинг+дев окружениях.

Интерфейс для просмотра макросов - [racktables.yandex-team.ru](https://racktables.yandex-team.ru). Там можно увидеть список входящих в макрос сетей и других макросов.

## Production

Макрос | Ссылка в racktables | Зачем нужен
:---: | :---: | :---:
`_VERTISPROD_` | ([racktables](https://racktables.yandex-team.ru/index.php?page=macros&macro_name=_VERTISPROD_)) | Наш главный композитный макрос для прода. Если нужен доступ для всех контейнеров или всех хостов - это нужный макрос
`_VERTISPRODNETS_)` | [racktables](https://racktables.yandex-team.ru/index.php?page=file&tab=default&file_id=12421) | Макрос для железных серверов, входит в `_VERTISPROD_`
`_CLOUD_YANDEX_CLIENTS_VERTISPROD_NETS_` | ([racktables](https://racktables.yandex-team.ru/index.php?page=file&tab=default&file_id=2850545)) | Макрос для облачных серверов в проде, входит в `_VERTISPROD_`
`_CLOUD_YANDEX_CLIENTS_VERTISPROD_LB_NETS_` | ([racktables](https://racktables.yandex-team.ru/index.php?page=file&tab=fw&file_id=2857864)) | Макрос для облачных серверов с выключенной опцией `superflow` в облаке, входит в `_VERTISPROD_`
`_CLOUD_YANDEX_CLIENTS_VERTISPROD_DUALSTACK_NETS_` | ([racktables](https://racktables.yandex-team.ru/index.php?page=file&tab=default&file_id=2857223)) | Макрос для облачных серверов с публичными ip-адресами, **не входит** в `_VERTISPROD_`

{% note warning %}

Мы не выдаем сетевые доступы от людей до макросов в проде никому, кроме нашей службы.

{% endnote %}

## Testing + dev

Макрос | Ссылка в racktables | Зачем нужен
:---: | :---: | :---:
`_VERTISDEV_` | ([racktables](https://racktables.yandex-team.ru/index.php?page=macros&macro_name=_VERTISDEV_)) | Композитный макрос для тестинга и дева. У всех вертикалей уже есть доступ к этому макросу.
`_VERTISDEVNETS_)` | [racktables](https://racktables.yandex-team.ru/index.php?page=file&file_id=11531) | Макрос для железных серверов, входит в `_VERTISDEV_`
`_CLOUD_YANDEX_CLIENTS_VERTISDEV_NETS_` | ([racktables](https://racktables.yandex-team.ru/index.php?page=file&tab=default&file_id=2848733)) | Макрос для облачных серверов в dev и тестинге, входит в `_VERTISDEV_`;
`_CLOUD_YANDEX_CLIENTS_VERTISDEV_LB_NETS_` | ([racktables](https://racktables.yandex-team.ru/index.php?page=file&tab=default&file_id=2857084)) | Макрос для облачных серверов в dev и тестинге с выключенной опцией `superflow` в облаке, входит в `_VERTISDEV_`;
`_CLOUD_YANDEX_CLIENTS_VERTISDEV_DUALSTACK_NETS_` | ([racktables](https://racktables.yandex-team.ru/index.php?page=file&tab=default&file_id=2857300)) | Макрос для облачных серверов с публичными ip-адресами, `не входит` в `_VERTISDEV_`.

## CME

Car.Market Expert живет в одном макросе для дев, тестинга и прода - `_CLOUD_YANDEX_CLIENTS_VERTISCME_NETS_`. Дырки от него нужно заказывать аккуратно и не заказывать дырки напрямую до вертикальных балансеров.

## Кондукторные макросы

Помимо сетевых макросов из racktables есть сетевые макросы по кондукторным группам из [c.yandex-team.ru](https://c.yandex-team.ru). Кондукторный макрос для группы можно узнать на странице группы в графе `Экспорт в фаервол`. Например, для группы [vertis_vprod_cme](https://c.yandex-team.ru/groups/vertis_vprod_cme) кондукторный макрос `_C_VERTIS_VPROD_CME_`.
