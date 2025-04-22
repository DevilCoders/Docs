## Promoter
Сервис предназначен для создания, получения и отображения аудитории бизнеса. 

* Описание сервиса [тут](https://wiki.yandex-team.ru/smb/product/clients/Vkladka-Lidy/)

#### Testing
api: http://promoter.tst.geosmb.maps.yandex.net
tvm: 2025906

#### Production
api: http://promoter.geosmb.maps.yandex.net
tvm: 2025904

* [ABC](https://abc.yandex-team.ru/services/maps-adv-clients-promoter/)
* Yav [testing](https://yav.yandex-team.ru/secret/sec-01ecw522mm6mxyhszwrhax1xv3) [production](https://yav.yandex-team.ru/secret/sec-01eeff5w12ratg9dg90qbn3jen)
* [CD](https://a.yandex-team.ru/ci/maps-adv-clients-promoter/releases/timeline?dir=maps_adv%2Fgeosmb%2Fpromoter%2Fserver&id=stable-release)
* [Sandbox resources](https://sandbox.yandex-team.ru/resources?type=GEOSMB_PROMOTER)
* [Deploy](https://deploy.yandex-team.ru/projects/geosmb-promoter)
* Awacs [testing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.tst.geosmb.slb.maps.yandex.net/show/) [production](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.geosmb.slb.maps.yandex.net/show/)
* YC [PostgreSQL](https://yc.yandex-team.ru/folders/foogmqqkbnujtjjq6n4p)
* Solomon [админка](https://solomon.yandex-team.ru/admin/projects/geosmb)

## API
Полные протоколы в директории `./proto/`

* `POST /v1/list_leads/` - получить список аудитории бизнеса.

input: **ListLeadsInput**

output: **ListLeadsOutput**

* `POST /v1/list_segments/` - получить список сегментов бизнеса с количеством лидов в каждом из них.

input: **ListSegmentsInput**

output: **ListSegmentsOutput**

* `POST /v1/retrieve_lead/` - получить данные лида.

input: **RetrieveLeadInput**

output: **Lead**

* `POST /v1/list_lead_events/` - получить список событий лида.

input: **ListLeadEventsInput**

output: **ListLeadEventsOutput**

* `POST /v1/list_lead_segments/` - получить список всех сегментов во всех бизнесах, в которые входит лид с переданными id.

input: **ListLeadSegmentsInput**

output: **ListLeadSegmentsOutput**

* `POST /internal/v1/search_leads_for_gdpr/` - GDPR only. Поиск лидов с указанным паспортом.

input: **SearchLeadsForGdprInput**

output: **SearchLeadsForGdprOutput**

* `POST /internal/v1/remove_leads_for_gdpr/` - GDPR only. Удаление данных лидов с указанным паспортом.

input: **RemoveLeadsForGdprInput**

output: **RemoveLeadsForGdprOutput**

