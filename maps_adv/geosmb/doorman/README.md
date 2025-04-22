## Doorman
Сервис предназначен для создания, получения и отображения клиентов бизнеса и их событий. [Описание](https://wiki.yandex-team.ru/smb/product/clients/Vkladka-klienty/)

#### Testing
api: http://doorman.tst.geosmb.maps.yandex.net
tvm: 2020024

#### Production
api: http://doorman.geosmb.maps.yandex.net
tvm: 2020026

* [ABC](https://abc.yandex-team.ru/services/maps-adv-doorman/)
* Yav [testing](https://yav.yandex-team.ru/secret/sec-01e0zf03dkndykq6ycyc1p8e89) [production](https://yav.yandex-team.ru/secret/sec-01e11e3xk9r3fgh3g3994z0jvf)
* [CD](https://a.yandex-team.ru/ci/maps-adv-doorman/releases/timeline?dir=maps_adv%2Fgeosmb%2Fdoorman%2Fserver&id=stable-release)
* [Sandbox resources](https://sandbox.yandex-team.ru/resources?type=GEOSMB_DOORMAN)
* [Deploy](https://deploy.yandex-team.ru/projects/geosmb-doorman)
* Awacs [testing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.tst.geosmb.slb.maps.yandex.net/show/) [production](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.geosmb.slb.maps.yandex.net/show/)
* YC [PostgreSQL](https://yc.yandex-team.ru/folders/foo718f3gn9888o4kpsj)
* Solomon [админка](https://solomon.yandex-team.ru/admin/projects/geosmb)


## Описание API
Полные протоколы в директории `./proto/`

* `POST /v1/create_client/` - создать клиента с переданными параметрами.

input: **ClientSetupData**

output: **ClientData**

* `POST /v1/create_clients/` - создание клиентов балком.

input: **BulkCreateClientsInput**

output: **BulkCreateClientsOutput**

* `POST /v1/retrieve_client/` - получить данные клиента.

input: **ClientRetrieveInput**

output: **ClientData**

* `POST /v1/list_clients/` - получить список клиентов бизнеса.

input: **ClientsListInput**

output: **ClientsListOutput**

* `POST /v1/list_suggest_clients/` - получить список клиентов бизнеса для саджеста. Выдаёт меньше данных, чем обычный листинг.

input: **ListSuggestClientsInput**

output: **ClientContactsList**

* `POST /v1/update_client/` - обновить данные клиента.

input: **ClientUpdateData**

output: **ClientData**

* `POST /v1/list_segments/` - получить список сегментов бизнеса с количеством клиентов в каждом из них.

input: **ListSegmentsInput**

output: **ListSegmentsOutput**

* `POST /v1/segment_statistics/` - получить динамику изменения сегмента бизнеса за последние 13 месяцев (включая текущий).

input: **SegmentStatisticsInput**

output: **SegmentStatisticsOutput**

* `POST /v1/list_clients_by_segment/` - получить список клиентов бизнеса в указанном сегменте.

input: **ClientsListBySegmentInput**

output: **ClientContactsList**

* `POST /v1/add_event/` - добавить событие клиента.

input: **AddEventInput**

output: **--**

* `POST /v1/list_client_segments/` - получить список всех сегментов во всех бизнесах, в которые входит клиент с переданными id.

input: **ListClientSegmentsInput**

output: **ListClientSegmentsOutput**

* `POST /internal/v1/search_clients_for_gdpr/` - проверить наличие клиентов по паспорту (для GDPR)

input: **SearchClientsForGdprInput**

output: **SearchClientsForGdprOutput**

* `POST /internal/v1/clear_clients_for_gdpr/` - удалить клиентов по паспорту (для GDPR)

input: **ClearClientsForGdprInput**

output: **ClearClientsForGdprOutput**
