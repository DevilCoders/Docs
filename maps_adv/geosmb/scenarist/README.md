## Scenarist
Сервис предназначен для подписок бизнеса на маркетинговые сценарии и последующих маркетинговых рассылок клиентам, попадающим в эти сценарии. 

* Описание инструментов маркетинга [тут](https://wiki.yandex-team.ru/smb/product/marketing/)
* Описание архитектуры сервиса, dataflow [тут](https://miro.com/app/board/o9J_ks05c8g=/)
* Дизайны фронта, который использует этот сервис [тут](https://www.figma.com/file/zhgG1jrUFTOWPifP9yfUnI/Marketing?node-id=675%3A0) 

#### Testing
api: http://scenarist.tst.geosmb.maps.yandex.net
tvm: 2021325

#### Production
api: http://scenarist.geosmb.maps.yandex.net
tvm: 2021327

* [ABC](https://abc.yandex-team.ru/services/maps-adv-clients-scenarist/)
* Yav [testing](https://yav.yandex-team.ru/secret/sec-01ecw70hmjc2610m8ny9xfep1z) [production](https://yav.yandex-team.ru/secret/sec-01eed4njd31em5dm9h502d2crt)
* [CD](https://a.yandex-team.ru/ci/maps-adv-clients-scenarist/releases/timeline?dir=maps_adv%2Fgeosmb%2Fscenarist%2Fserver&id=stable-release)
* [Sandbox resources](https://sandbox.yandex-team.ru/resources?type=GEOSMB_SCENARIST)
* [Deploy](https://deploy.yandex-team.ru/projects/geosmb-scenarist)
* Awacs [testing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.tst.geosmb.slb.maps.yandex.net/show/) [production](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.geosmb.slb.maps.yandex.net/show/)
* YC [PostgreSQL](https://yc.yandex-team.ru/folders/foo0kslu1fr3ghotcst0)
* Solomon [админка](https://solomon.yandex-team.ru/admin/projects/geosmb)


## API
Полные протоколы в директории `./proto/`

* `POST /v1/list_scenarios/` - список всех сценариев с подписками текущего бизнеса.

input: **scenarios.ListScenariosInput**

output: **scenarios.ListScenariosOutput**

* `POST /v1/create_subscription/` - создание подписки на сценарий.

input: **scenarios.CreateSubscriptionInput**

output: **scenarios.SubscriptionSchema**

* `POST /v1/retrieve_subscription/` - инфа о подписке.

input: **scenarios.RetrieveSubscriptionInput**

output: **scenarios.RetrieveSubscriptionOutput**

* `POST /v1/update_subscription_status/` - Изменить статус подписки.

input: **scenarios.UpdateSubscriptionStatusInput**

output: --

* `POST /v1/replace_subscription_coupon/` - Обновление купона подписки.

input: **scenarios.ReplaceCouponInput**

output: **scenarios.ReplaceCouponOutput**

