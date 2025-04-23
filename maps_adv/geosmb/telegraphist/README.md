## Telegraphist
Сервис отправки уведомлений. На данный момент поддерживаются:
* отправка уведомления о покупке сертификата по явно указанному адресу почты (`api/v1/...`).
* отправка уведомлений о записи по почте, смс, пушом (`api/v2/...`).

#### Testing
api: http://telegraphist.tst.geosmb.maps.yandex.net
tvm: 2023888

#### Production
api: http://telegraphist.geosmb.maps.yandex.net
tvm: 2023886

* [ABC](https://abc.yandex-team.ru/services/maps-adv-clients-telegraphist/)
* Yav [testing](https://yav.yandex-team.ru/secret/sec-01edvgjvqchvnmvtdcw2g16v78), [production](https://yav.yandex-team.ru/secret/sec-01eefn1de5pg4jk46emcf21d6c)
* [CD](https://a.yandex-team.ru/ci/maps-adv-clients-telegraphist/releases/timeline?dir=maps_adv%2Fgeosmb%2Ftelegraphist%2Fserver&id=stable-release)
* [Sandbox resources](https://sandbox.yandex-team.ru/resources?type=GEOSMB_TELEGRAPHIST)
* [Deploy](https://deploy.yandex-team.ru/projects/geosmb-telegraphist)
* Awacs [testing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.tst.geosmb.slb.maps.yandex.net/show/) [production](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.geosmb.slb.maps.yandex.net/show/)
* Solomon [админка](https://solomon.yandex-team.ru/admin/projects/geosmb)
* Рассылятор [testing](https://test.sender.yandex-team.ru/clients/), [production](https://test.sender.yandex-team.ru/clients/)

## API
Протоколы живут в `./proto/`.

#### Отправка уведомления

`POST /api/v1/send-notification/`

input: **notifications_v1.EmailNotification**

output:
* **HTTP 204** - уведомление успешно отправлено
* **HTTP 400, Error** - ошибка валидации
* **HTTP 406, Error** - отправка уведомления указанному получателю ограничена администратором

#### Отправка уведомления v2

`POST /api/v2/send-notification/`

input: **notifications_v2.Notification**

output:
* **HTTP 200, common.NotificationResult** - список **common.NotificationTransportResult**, описывающих результат попытки отправить сообщение по каждому переданному транспорту.
    * если `common.NotificationTransportResult` содержит `error`, то что-то пошло не так.
    * если `common.NotificationTransportResult` содержит `effective_address`, то всё получилось.
* **HTTP 400, Error(code=errors.VALIDATION_ERROR)** - ошибка валидации входящих данных
* **HTTP 400, Error(code=errors.UNSUPPORTED_TRANSPORT)** - переданный транспорт не поддерживается. Какой именно из переданных транспортов не поддерживается указано в `description`.
* **HTTP 400, Error(code=errors.NO_ORGS_FOR_BIZ_ID)** - не смогли получить данные об организации в геопоиске
* **HTTP 400, Error(code=errors.NO_ORG_INFO)** - не смогли получить данные об организации в BVM
* **HTTP 406, Error(code=errors.RECIPIENT_DENIED)** - отправка уведомления указанному получателю ограничена администратором


`POST /api/v2/send_notification_for_business/`

input: **notifications_for_business.Notification**

output:
* **HTTP 200, common.NotificationResult** - список **common.NotificationTransportResult**, описывающих результат попытки отправить сообщение по каждому переданному транспорту.
    * если `common.NotificationTransportResult` содержит `error`, то что-то пошло не так.
    * если `common.NotificationTransportResult` содержит `effective_address`, то всё получилось.
* **HTTP 400, Error(code=errors.VALIDATION_ERROR)** - ошибка валидации входящих данных
* **HTTP 400, Error(code=errors.UNSUPPORTED_TRANSPORT)** - переданный транспорт не поддерживается. Какой именно из переданных транспортов не поддерживается указано в `description`.
* **HTTP 400, Error(code=errors.UNKNOWN_CLIENT)** - не смогли найти клиента в Doorman
* **HTTP 400, Error(code=errors.NO_ORGS_FOR_BIZ_ID)** - не смогли получить данные об организации в геопоиске
* **HTTP 400, Error(code=errors.NO_ORG_INFO)** - не смогли получить данные об организации в BVM
* **HTTP 406, Error(code=errors.RECIPIENT_DENIED)** - отправка уведомления указанному получателю ограничена администратором


#### Отправка уведомления v3

`POST /api/v3/send-notification/`

input: **notifications_v3.Notification**

output:
* **HTTP 200, common_v3.NotificationResult** - список **common_v3.NotificationTransportResult**, описывающих результат попытки отправить сообщение по переданному транспорту.
    * если `common.NotificationTransportResult` содержит `error`, то что-то пошло не так.
    * если `common.NotificationTransportResult` содержит `effective_address`, то всё получилось.
* **HTTP 400, Error(code=errors.VALIDATION_ERROR)** - ошибка валидации входящих данных
* **HTTP 400, Error(code=errors.UNSUPPORTED_TRANSPORT)** - переданный транспорт не поддерживается. Какой именно из переданных транспортов не поддерживается указано в `description`.
* **HTTP 406, Error(code=errors.RECIPIENT_DENIED)** - отправка уведомления указанному получателю ограничена администратором


## Важно
Рассылятор использует те шаблоны, которые сохранены непосредственно в нём. Шаблоны
в server/lib/templates/email используются только для истории версий, изменение и
перевыкатка приложения никак не повлияют на макеты отправляемых транзакционных писем.
Если нужно что-то поменять в шаблонах - _**убедительно**_ прошу внести эти изменения
сюда. Правильная последовательность действий:
- внести изменения;
- проверить, что шаблон успешно обрабатывается шаблонизатором (jinja);
- собрать архивы с шаблонами (командой, описанной ниже);
- загрузить полученный(е) архив(ы) через веб-интерфейс Рассылятора.

## Сборка архивов для Рассылятора
HTML-письма в Рассылятор удобнее всего загружать в виде zip-архива.
Чтобы создать из шаблонов подходящие архивы, нужно выполнить команду `make zips`.
Полученные архивы можно загружать в Рассылятор через web-интерфейс при создании
транзакционной рассылки или нового её варианта. 
