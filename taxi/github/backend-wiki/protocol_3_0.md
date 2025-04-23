# Клиентский протокол

# Оглавление

* <a href="#version">Версия</a>
* <a href="#changelog">История изменений</a>
* <a href="#formatting">Условные обозначения</a>
* <a href="#changes_2x">Основные отличия от версий 2.х</a>
* <a href="#userid">Идентификаторы пользователей</a>
* <a href="#statuses">Статусы заказов</a>
* <a href="#proxies">Проксируемые запросы</a>
* <a href="#block">Блокировка пользователя</a>
* <a href="#localization">Локализация</a>
* <a href="#additional_types">Дополнительные типы данных</a>
* <a href="#request_add_user_message">add_user_message</a>
* <a href="#request_allcars">allcars</a>
* <a href="#request_auth">auth</a>
* <a href="#request_authconfirm">authconfirm</a>
* <a href="#request_cards">cards</a>
* <a href="#request_changeaction">changeaction</a>
* <a href="#request_changecomment">changecomment</a>
* <a href="#request_changecorpcostcenter">changecorpcostcenter</a>
* <a href="#request_changedestinations">changedestinations</a>
* <a href="#request_changepayment">changepayment</a>
* <a href="#request_changeporchnumber">changeporchnumber</a>
* <a href="#request_changes">changes</a>
* <a href="#request_cities">cities</a>
* <a href="#request_couponcheck">couponcheck</a>
* <a href="#request_deptranscars">deptranscars</a>
* <a href="#request_email">email</a>
* <a href="#request_feedback">feedback</a>
* <a href="#request_freecars">freecars</a>
* <a href="#request_geomagnet">geomagnet</a>
* <a href="#request_geosearch">geosearch</a>
* <a href="#request_get_user_messages">get_user_messages</a>
* <a href="#request_get_user_settings">get_user_settings</a>
* <a href="#request_getreferral">getreferral</a>
* <a href="#request_launch">launch</a>
* <a href="#request_lbs">lbs</a>
* <a href="#request_nearestparks">nearestparks</a>
* <a href="#request_nearestposition">nearestposition</a>
* <a href="#request_nearestzone">nearestzone</a>
* <a href="#request_order">order</a>
* <a href="#request_ordercommit">ordercommit</a>
* <a href="#request_orderdraft">orderdraft</a>
* <a href="#request_orderhistory">orderhistory</a>
* <a href="#request_parkdetails">parkdetails</a>
* <a href="#request_paymentmethods">paymentmethods</a>
* <a href="#request_paymentstatuses">paymentstatuses</a>
* <a href="#request_payorder">payorder</a>
* <a href="#request_pickuppoints">pickuppoints</a>
* <a href="#request_pricecat">pricecat</a>
* <a href="#request_promotions">promotions</a>
* <a href="#request_pushack">pushack</a>
* <a href="#request_reorder">reorder</a>
* <a href="#request_routestats">routestats</a>
* <a href="#request_save_user_settings">save_user_settings</a>
* <a href="#request_setdontcall">setdontcall</a>
* <a href="#request_setdontsms">setdontsms</a>
* <a href="#request_sharedroute">sharedroute</a>
* <a href="#request_sharedroutetrack">sharedroutetrack</a>
* <a href="#request_suggesteddestinations">suggesteddestinations</a>
* <a href="#request_suggestedpositions">suggestedpositions</a>
* <a href="#request_tariffs">tariffs</a>
* <a href="#request_tariffzonemap">tariffzonemap</a>
* <a href="#request_taxicount">taxicount</a>
* <a href="#request_taxiontheway">taxiontheway</a>
* <a href="#request_taxiroute">taxiroute</a>
* <a href="#request_taxisearch">taxisearch</a>
* <a href="#request_translations">translations</a>
* <a href="#request_updatetips">updatetips</a>
* <a href="#request_userplacenew">userplacenew</a>
* <a href="#request_userplaces">userplaces</a>
* <a href="#request_userplacesimport">userplacesimport</a>
* <a href="#request_userplacesremove">userplacesremove</a>
* <a href="#request_userplacesupdate">userplacesupdate</a>
* <a href="#request_weathersuggest">weathersuggest</a>
* <a href="#request_zoneinfo">zoneinfo</a>



<a name="version"></a>
## Версия 3.0.44

При обратно-совместимых изменениях увеличивается самый младший номер версии протокола.
В этом случае протокол будет записан на этой же странице вместо предыдущей версии
с указанием изменений.

Обратно-совместимыми изменениями считаются:

* добавление параметров в запрос или ответ
* добавление новых видов запросов

При обратно-несовместимых изменениях, если уже выпущено хотя бы одно приложение
на этой версии протокола, увеличивается средний номер. В этом случае протокол
будет записан на новой странице. Все версии протокола, кроме самой свежей,
поддерживаются только в режиме устранения критических багов.


<a name="changelog"></a>
## История изменений

* 3.0.1
    * в запрос `launch` добавлен параметр `mpns_url`
* 3.0.2
    * добавлено описание проксируемого запроса `geosuggest`
    * в запрос `launch` добавлен параметр `yandex_staff`
* 3.0.3 **обратная несовместимость**
    * параметр `yamoney` перенесен из запроса `launch` в раздел `requirements` запроса `cities`
    * из запроса `launch` удален обязательный параметр `city`
* 3.0.4
    * в ответ `cities` добавлен параметр `tz`
    * в ответе `pricecat` в значение параметра `parks.0.tariffs.taximeter.intervals` добавлен параметр `schedule`
* 3.0.5
    * в ответ `cities` в значение параметра `hotspots.0` добавлен параметр `radius`
* 3.0.6
    * добавлено описание запроса `nearestparks`
* 3.0.7
    * в ответ `taxisearch` добавлен параметр `request`
* 3.0.8
    * в ответе `parkdetails` параметр `included` заменён на `prepaid`
    * в ответе `pricecat.tariffs.O` остались только `id` и `class`
* 3.0.9 **обратная несовместимость**
    * удалены варианты пожеланий клиента `card`, `newspaper`, `wifi`
* 3.0.10 **обратная несовместимость**
    * изменился формат ответа `pricecat` и `parkdetails`
* 3.0.11 **обратная несовместимость**
    * переработан запрос `routehistory`
* 3.0.12 **обратная несовместимость**
    * из ответа ручки `routestats` пропали поля `min_price`, `max_price`, `min_delta` и `cars`
* 3.0.13 **обратная несовместимость**
    * изменилось поле `0.areas.area_id.name` в ответе ручки `cities`
    * убрали все поля типа `i18n`
* 3.0.14
    * в ответ ручки `routestats` добавлено поле `calc_by_class`
* 3.0.15
    * в параметры запроса ручки `launch` добавлено поле `gcm_token`
* 3.0.16
    * в документацию на ручки `order`, `taxisearch`, `taxiontheway` и в дополнительные типы данных добавлены купоны
* 3.0.17
    * в ответ ручки `routestats` добавлено поле `cars`
    * в ответ ручки `cities` добавлено поле `currency`
* 3.0.18
    * во всех запросах разрешено передавать параметр `id`
* 3.0.19
    * зафиксирована длина и набор символов кода подтверждения авторизации
* 3.0.20
    * в запрос ручки `order` добавлено поле `service_level`
    * в ответ ручки `taxiontheway` добавлено поле `cost_message`
* 3.0.21 **обратная несовместимость**
    * в запросе ручки `routestats` изменились требования к обязательности полей
    * в ответе ручки `routestats` удалены поля `cars`, `calc_by_class`
    * в ответе ручки `routestats` изменены поля `calc`, `distance`, `time`
    * в ответах ручек `routestats` и `cities` добавлено поле `service_levels`
    * в запросы ручек `freecars` и `taxicount` добавлено поле `service_levels`
* 3.0.22 **обратная несовместимость**
    * из ответа `cities` удалены поля `currency` и `areas`
* 3.0.23
    * время подачи `due` в запросе `order` стало необязательным параметром
* 3.0.24
    * в ответ ручки `geosearch` добавлено поле `description`
* 3.0.25
    * в ответ `cities.hotspots.0` добавлено поле `description`
* 3.0.26
    * в ответ `cities.service_levels.0` добавлено поле `description`
    * в ответ `routestats.service_levels.0` добавлено поле `description`
* 3.0.27
    * удалена поддержка поля `description`, добавленная в 3.0.26
* 3.0.28
    * в ответ `cities` добавлено поле `geo_id`
* 3.0.29
    * добавлена ручка `nearestposition`
    * добавлена ручка `suggesteddestinations`
* 3.0.30
    * в ответ ручки `taxiontheway` добавлено поле `routeinfo`
* 3.0.31
    * в ответ ручки `cities` добавлены поля `max_tariffs_url`, `max_tariffs`
* 3.0.32
    * в ответ ручки `launch` добавлено поле `blocked`
* 3.0.33
    * добавлена ручка `couponcheck`
* 3.0.34
    * дописаны поля ручки `order`
* 3.0.35
    * в ручке `parkdetails` в поле `tariffs` у услуг и групп услуг добавлен параметр `id`
    * в ручке `cities` у каждого города с МРТ в поле `max_tariffs` у услуг и групп услуг добавлен параметр `id`
* 3.0.36
    * в ответ `routestats` добавлено поле `service_levels.0.description_parts`
* 3.0.37
    * в ответ ручки `couponcheck` добавлено поле `details`, содержащее дополнительные сведения о купоне
    * в ручке `routestats` появилась возможность передавать купон и получать о нем информацию
    * добавлен код ответа 423 Locked    
* 3.0.38
    * все ручки проверяют наличие и валидность токена, если пользователь ранее авторизовался по нему
    * добавлены коды ответа `406 Not Acceptable`, если токен валиден, но не подходит
* 3.0.39
    * добавлены ручки `updatetips`, `paymentstatuses` и `payorder`
    * ручка `feedback` принимает новый параметр `tips`
    * ручка `launch` возращает новое поле `payment_statuses_filter`
    * расширены коды ответов `updated_requirements.reason.code` в ответе
      ручек `taxisearch` и `taxiontheway`
    * ручка `taxiontheway` возвращает новое поле `tips`
* 3.0.40
    * Добавлена ручка email
* 3.0.41
    * добавлена ручка `weathersuggest`
* 3.0.42
    * запрос ручки `order` и ответ ручки `taxiontheway` (и `taxisearch`)
      расширены параметром `dont_call`
* 3.0.43
    * ответ ручек `taxisearch` и `taxiontheway` расширен полем
      `cancelled_by` с возможными значениями: `"user"`, `"park"`
* 3.0.44
    * добавлена ручка `geomagnet`

<a name="formatting"></a>
## Условные обозначения

Значение каждого ключа JSON может быть описано тремя параметрами:

* `t: допустимые/типы/данных`
* `f: формат`
* `v: допустимые/значения`
* `r: регулярное выражение`

Например:

* `t: string` `f: date-time` строка, содержащая дату и время в формате ISO 8601
* `t: boolean/integer` `v: true/false/1/2/3` либо логическое значение истина/ложь, либо целое число от 1 до 3

Обязательные параметры помечены ⋮странными ⋮точками.


<a name="changes_2x"></a>
## Основные отличия от версий 2.х

* Типы данных приведены к наиболее подходящим по смыслу. Например, логические параметры
  вместо строк `"1"` и `"0"` теперь имеют значения `true` и `false`.

* Из протокола исключены устаревшие неиспользуемые виды запросов.


<a name="userid"></a>
## Идентификаторы пользователей

Идентификатор пользователя - это случайный уникальный идентификатор сессии, который генерируется
сервером при запросе `launch` и позволяет отслеживать все запросы одного и того же пользователя, в
том числе аутентифицировать пользователя для создания заказа.

Клиентское приложение должно передавать идентификатор во всех запросах к серверу, если
идентификатор уже известен (запрос `launch` завершился успешно). Допускается не передавать `id` в
тех случаях, когда он не является обязательным параметром запроса, для ускорения инициализации
приложения и реакции на действия пользователя (например, при первом запуске приложения в запросе
`cities` для определения города).


<a name="statuses"></a>
## Статусы заказов

Каждый заказ в Яндекс.Такси проходит через строго определенную цепочку этапов. Эти этапы
обозначаются особыми ключевыми словами, которые имеют одинаковое значение во всех запросах протокола:

* `scheduling` (только для заказов на точное время)

  Заказ уже предложен партнерам, но на него еще не назначен ни конкретный водитель,
  ни конкретная компания. Заказ может находиться в этом состоянии достаточно долго -
  например, при заказе на завтрашее утро заказ может находиться в этом состоянии всю ночь.

* `scheduled` (только для заказов на точное время)

  Заказ уже закреплен за конкретной компанией и конкретным водителем, но водитель
  еще не выехал к клиенту. Партнер может за много часов взять на себя обязательство
  выполнить заказ, но при этом сервер Яндекс.Такси не будет показывать клиенту
  перемещения водителя по городу все это время. Заказ может находиться в этом состоянии
  достаточно долго, аналогично `scheduling`.

* `search` (только для срочных заказов)

  Заказ уже предложен ближайшим к пользователю водителям, но ни один из них
  еще не согласился его выполнить. Заказ может находиться в этом состоянии не более 15 минут.

* `driving`

  Водитель едет к клиенту.

* `waiting`

  Водитель ожидает клиента возле места подачи.

* `transporting`

  Водитель забрал клиента и выполняет заказ.

* `complete`

  Водитель успешно выполнил заказ.

* `failed`

  Заказ сорван по вине компании-партнера. Заказ может попасть это состояние из любого другого.

* `cancelled`

  Заказ отменен клиентом (независимо от того, сделано это через приложение или через
  диспетчера/водителя). Заказ может попасть в это состояние из любого другого.

* `expired` и `preexpired`

  Если на заказ не найден исполнитель, это состояние означает, что прошло слишком много
  времени, и поиск водителя прекращен. Если на заказ исполнитель найден, это состояние
  означает, что произошел технический сбой и реальное состояние заказа неизвестно
  (партнер не присылал обновления состояния в течение длительного времени).
  В обоих случаях заказ считается завершенным.


<a name="proxies"></a>
## Проксируемые запросы

Часть запросов не обрабатывается непосредственно серверами Яндекс.Такси, а проксируется
во внешние сервисы. Для таких запросов мы не можем предоставить схему, набор параметров
или примеры использования, а только даем ссылку на внешнюю документацию.

*  `geosuggest` http://wiki.yandex-team.ru/SERP/suggest/geo


<a name="block"></a>
## Блокировка пользователя

В ответ на любой запрос клиента, содержащий id пользователя, сервер может сообщить о том,
что этот пользователь заблокирован в системе за нарушения до определенной даты.
Блокировка бывает двух типов - по id клиента и по его номеру телефона - сервер сообщает
тип в параметре `type`. Если клиент заблокирован по id, то он не сможет совершать
попытки авторизации телефона с этим id. При этом клиент может получить новый
незаблокированный id в `launch`. Если клиент заблокирован по номеру телефона,
то на этот номер телефона будет невозможно отправлять заказы. В этом случае
получение нового id не приведет к разблокировке номера телефона.

Формат ответа указан в разделе <a href="#additional_types">Дополнительные типы данных</a>.


<a name="localization"></a>
## Локализация
Клиент может указать, на каком языке он хотел бы получить ответ. Язык указывается
в HTTP-заголовке `Accept-Language`.
Формат заголовка стандартный. Сервер берет из заголовка первый знакомый ему язык и использует его.
На текущий момент поддерживаются языки `ru` и `en`. Если заголовок не передан, используется `ru`.
Если передан, но ни одного из поддерживаемых языков там нет, используется `en`.


<a name="token_authorization"></a>
##Авторизация по токену
Если клиент поддерживает создание аккаунта и авторизацию через аккаунт-менеджер (АК),
то он должен передавать полученный от АК токен во все ручки протокола 3.0 в виде заголовка
`Authorization: Bearer TOKEN_FROM_ACCOUNT_MANAGER`.

Первый запрос с токеном должен осуществляться в ручку `launch`, при этом если к аккаунту
уже привязан и подтвержден номер телефона, то подтверждение номера телефона старым способом
(через `auth`/`authconfirm`) не требуется — ручка `launch` вернет номер телефона по умолчанию,
список привязанных в Паспорте (незаблокированных) телефонов и поле `authorized: True`.

Клиент может изменить номер телефона на другой подтвержденный в Паспорте номер через ручку `auth`.
При этом код подтверждения не высылается, возвращается поле `authorized: True`.

Если клиент, авторизованный по токену, сделает запрос в любую другую ручку без токена, сервер
ответит ошибкой `400 Bad Request` с телом вида:

-

    {
        "error": {
            "code": "MISSING_TOKEN",
            "text": "Некоторый человекочитаемый текст ошибки"
        }
    }

Если клиент, ранее авторизованный по токену, придет без токена в ручку `launch`,
то его авторизация будет снята, и из профиля пользователя будет удалена информация о ранее
сохраненном телефоне и аккаунте Паспорта. После этого данный клиент может приходить в ручки
как обычный старый клиент без токена (предварительно пройдя авторизацию по старой схеме через
`auth`/`authconfirm`).

Если клиент передаст невалидный токен, то сервер ответит ошибкой `401 Unauthorized`,
поле `code` будет содержать строку `INVALID TOKEN`. Такая же ошибка будет возвращаться при запросе
без токена в ручках, обязательно требующих токен
(новые ручки, связанные с оплатой картой: на данный момент только `cards`).

Кроме того, при запросе с токеном сервер может вернуть ошибку `406 Not Acceptable`
такого же формата в следующих случаях (на тип ошибки указывает значение поля `code`):
 
 - UID_DOES_NOT_MATCH - uid, для которого выдан токен, не совпадает с uid,
   сохраненным для данного id клиента;
 - MISSING_UID - у данного id клиент отсутствует сохраненный uid
 - UNKNOWN_PHONE - телефон, ранее привязанный к данному id клиента, не известен Паспорту
   (заблокирован, отвязан и т.п.); проверяется только в некоторых ручках (на данный момент это
   `launch`, `order` и `cards`).

<a name="additional_types"></a>
## Дополнительные типы данных
### address
   `t: object`     адрес
*   ⋮ __city__ `t: string`     город
*   ⋮ __country__ `t: string`     страна
*   ⋮ __exact__ `t: boolean`     точно ли определен адрес
*   ⋮ __full_text__ `t: string`     полный адрес
*   ⋮ __house__ `t: string`     дом
*   ⋮ __object_type__ `t: string` `v: аэропорт/организация/другое`    классификация объекта или организации
*   ⋮ __point__ `t: point`     координаты объекта или организации
    *   ⋮ __response__ `t: point`     объект ответа целиком
*   ⋮ __short_text__ `t: string`     короткий адрес
*   ⋮ __street__ `t: string`     улица
*   ⋮ __type__ `t: string` `v: address/organization`    тип объекта - адрес или организация
*    __comment__ `t: string`     комментарий к заказу
*    __description__ `t: string`     мелко-подробности
*    __oid__ `t: string`     идентификатор объекта
*    __porchnumber__ `t: string`     подъезд
*    __short_text_from__ `t: string`     короткий адрес после предлога ОТ (откуда)
*    __short_text_to__ `t: string`     короткий адрес после предлога ДО (куда)
*    __tag__ `t: string`     тэг

### area
   `t: string`   `r: [a-z0-9_-]+`  идентификатор трансферной или тарифной зоны (уникален в пределах города)

### blocked
   `t: object`     пользователь заблокирован
*   ⋮ __blocked__ `t: string`  `f: date-time`   время окончания блокировки
*   ⋮ __type__ `t: string` `v: id/phone`    тип блокировки

### change_action
   `t: object`     действие по изменению заказа
*   ⋮ __name__ `t: string` `v: user_ready/porchnumber/comment/destinations/payment`    название действия

### change_object
   `t: `     объект-изменение
*   ⋮ __change_id__ `t: /#definitions/uuid4`     id изменения
    *   ⋮ __response__ `t: /#definitions/uuid4`     объект ответа целиком
*   ⋮ __name__ `t: string`     название изменения
*   ⋮ __status__ `t: /#definitions/change_status`     статус изменения
    *   ⋮ __response__ `t: /#definitions/change_status`     объект ответа целиком
*   ⋮ __value__ `t: object`     значение изменения

### change_status
   `t: string` `v: pending/success/failed`    статус изменения

### city
   `t: string`  `f: city`   название города (только такого, в котором можно заказать Яндекс.Такси)

### class
   `t: array`     класс автомобиля по категориям Яндекс.Такси
*   ⋮ __response__ `t: tariff_class`     объект ответа целиком

### coupon_info
   `t: object`     информация о купоне
*   ⋮ __valid__ `t: boolean`     купон принят к оплате
*    __valid_any__ `t: boolean`     купон не принят к оплате, но может быть принят в другом заказе
*    __value__ `t: number`     номинал купона (только если принят)
*    __value_as_str__ `t: string`     номинал купона с валютой (только если принят)

### coupon_request
   `t: string`     купон в запросе

### currency
   `t: string`     валюта

### currency_rules
   `t: object`     правила показа валюты
*   ⋮ __code__ `t: string`     код валюты
*   ⋮ __template__ `t: string`     шаблон для отображения валюты
*   ⋮ __text__ `t: string`     краткое название валюты, которое клиент использует, если не может отобразить знак
*    __sign__ `t: string`     знак валюты, который клиент отображает, если может

### distance
   `t: number`     единица измерения расстояния

### email
   `t: string`  `f: email`  `min-length: 5` адрес электронной почты

### email_action
   `t: string` `v: get/set/unset/confirm`    действие над адресом электронной почты

### email_status
   `t: string` `v: ok/confirmation_sent/confirmation_error/not_confirmed`    статус адреса электронной почты

### error_response
   `t: object`     ответ в случае ошибки
*    __error__ `t: object`     код и текст ошибки
    *    __code__ `t: string`    `min-length: 6` текстовый код ошибки, например: INVALID_TOKEN
    *    __text__ `t: string`    `min-length: 12` человекопонятное описание ошибки для показа пользователю

### excluded_parks
   `t: array`     список идентификаторов таксопарков

### feedback_choices
   `t: object`     Возможные варианты фидбека

### feedback_rating
   `t: integer`     оценка по пятибалльной шкале

### forwarding
   `t: object`     номер телефона через шлюз переадресации
*   ⋮ __ext__ `t: string`   `r: \d{4,5}`  добавочный номер через шлюз переадресации
*   ⋮ __phone__ `t: string`   `r: \+\d{11,}|8\d{10,}`  номер телефона шлюза в международном формате

### fullscreen_banner
   `t: object`     полноэкранный баннер
*   ⋮ __caption__ `t: string`     заголовок
*   ⋮ __end_date__ `t: string`  `f: date-time`   дата окончания действия
*   ⋮ __id__ `t: string`     идентификатор баннера
*   ⋮ __image__ `t: image`     изображение на баннере
    *   ⋮ __response__ `t: image`     объект ответа целиком
*   ⋮ __priority__ `t: integer`     приоритет показа
*   ⋮ __screen__ `t: string`     экран показа баннера
*   ⋮ __start_date__ `t: string`  `f: date-time`   дата начала действия
*   ⋮ __text__ `t: string`     текст
*   ⋮ __widgets__ `t: object`     кнопки, которые должны быть на баннере
    *    __action_button__ `t: object`     кнопка внизу баннера
        *   ⋮ __deeplink__ `t: [u'string', u'null']`     диплинк кнопки
        *   ⋮ __label__ `t: string`     локализованный текст кнопки
        *    __target__ `t: [u'string']`     цель для диплинка, e.g. webview
    *    __close_button__ `t: boolean`     должен ли пристутствовать крестик
    *    __menu_button__ `t: boolean`     должна ли присутствовать кнопка меню
*    __cities__ `t: array`     города, в которых действует баннер
    *   ⋮ __response__ `t: city`     объект ответа целиком
*    __promotion__ `t: string`     промоакция, связанная с баннером

### home_zone_name
   `t: string`     ?

### image
   `t: object`     изображение для вывода на клиенте
*   ⋮ __url__ `t: string`     URL изображения
*    __size_hint__ `t: integer`     число, обозначающее желаемый размер (смысл значения зависит от клиента)

### intermediary
   `t: string` `v: terminal/callcenter/partner`    тип посредника для заказа

### order_status
   `t: string` `v: scheduling/scheduled/search/driving/waiting/transporting/complete/failed/cancelled/preexpired/expired`    статус заказа (см. соответствующий раздел)

### overprices
   `t: array`     список услуг, за которые взымается дополнительная плата
*   ⋮ __name__ `t: string`     название услуги
*   ⋮ __price__ `t: price`     стоимость оказания услуги
    *   ⋮ __response__ `t: price`     объект ответа целиком

### payment
   `t: object`     данные для оплаты картой (только при requirements.creditcard=true)
*    __cardid__ `t: string`  `f: payment_id`  `min-length: 6` id карты из ручки cards
*    __payment_method_id__ `t: payment_method_id`     ?
    *   ⋮ __response__ `t: payment_method_id`     объект ответа целиком
*    __tips__ `t: tips`     чаевые по умолчанию
    *   ⋮ __response__ `t: tips`     объект ответа целиком
*    __type__ `t: payment_method`     ?
    *   ⋮ __response__ `t: payment_method`     объект ответа целиком

### payment_method
   `t: string` `v: cash/card/corp/applepay`    ?

### payment_method_id
   `t: string`  `f: payment_id`  `min-length: 6` способ оплаты

### payment_statuses_filter
   `t: array`     типы платежей, которые можно отразить в paymentstatuses

### phone
   `t: string`   `r: \+\d{11,}(,\d{4,})?|8\d{10,}(,\d{4,})?`  номер телефона в международном формате (прямой номер или через шлюз, с добавочным номером через ","

### point
   `t: array`     геокоординаты точки

### polygon
   `t: array`     полигон, последовательность точек
*   ⋮ __response__ `t: point`     объект ответа целиком

### position
   `t: object`     местоположение устройства
*    __dx__ `t: integer`     погрешность местоположения в метрах
*    __point__ `t: point`     ?
    *   ⋮ __response__ `t: point`     объект ответа целиком

### price
   `t: integer`     стоимость чего-либо или цена чего-либо

### prices
   `t: array`     стоимость проезда по маршруту
*   ⋮ __extra__ `t: array`     оплата времени или расстояния по маршруту сверх включенного в минимальную стоимость поездки
    *    __length__ `t: distance`     единица измерения расстояния, за которое берётся доплата; округляется до заданного числа в большую сторону
        *   ⋮ __response__ `t: distance`     объект ответа целиком
    *    __price__ `t: price`     стоимость доплаты за время или расстояние, пройденное сверх включенного в минимальную стоимость значения
        *   ⋮ __response__ `t: price`     объект ответа целиком
    *    __time__ `t: time`     единица измерения времени, за которое берётся доплата; округляется до заданного числа в большую сторону
        *   ⋮ __response__ `t: time`     объект ответа целиком
*    __area__ `t: area`     тарифная или трансферная зона, через которую прошла часть маршрута
    *   ⋮ __response__ `t: area`     объект ответа целиком
*    __prepaid__ `t: object`     включенное в минимальную стоимость время и/или расстояние
    *    __length__ `t: distance`     включенное в минимальную стоимость расстояние
        *   ⋮ __response__ `t: distance`     объект ответа целиком
    *    __time__ `t: time`     включенное в минимальную стоимость время
        *   ⋮ __response__ `t: time`     объект ответа целиком

### promocode_referral
   `t: object`     ?
*   ⋮ __currency__ `t: string`     код валюты (нужен старым клиентам)
*   ⋮ __descr__ `t: string`     описание промокода (для меню)
*   ⋮ __message__ `t: string`     описание промокода (для отправки в соц. сети)
*   ⋮ __promocode__ `t: coupon_request`     код купона
    *   ⋮ __response__ `t: coupon_request`     объект ответа целиком
*   ⋮ __rides_count__ `t: integer`     полное число поездок по промокоду
*   ⋮ __rides_left__ `t: integer`     оставшееся число поездок по промокоду
*   ⋮ __value__ `t: integer`     номинал промокода
*    __currency_rules__ `t: currency_rules`     данные о валюте заказа (если клиент запросил)
    *   ⋮ __response__ `t: currency_rules`     объект ответа целиком

### promotion
   `t: object`     информация о промо-акции
*    __action__ `t: object`     Действие, связанное с промо-акцией
    *   ⋮ __deeplink__ `t: string`     диплинк действия
    *    __target__ `t: string`     цель для диплинка, e.g. webview
*    __cities__ `t: array`     список названий городов, поддерживающих эту промо-акцию
    *   ⋮ __response__ `t: city`     объект ответа целиком
*    __name__ `t: string`     идентификатор промо-акции

### promotion_list
   `t: array`     список промо-акций
*   ⋮ __response__ `t: promotion`     объект ответа целиком

### reorder_suggestion
   `t: object`     предложение по изменению параметров заказа
*   ⋮ __cancel_button_title__ `t: string`     заголовок кнопки отказа от изменения параметров заказа
*   ⋮ __message__ `t: string`     текст сообщения
*   ⋮ __options__ `t: array`     список предлагаемых пользователю вариантов
    *   ⋮ __button_title__ `t: string`     заголовок кнопки выбора предложенного изменения
    *   ⋮ __decision_id__ `t: string`     идентификатор предлложенного изменения
*   ⋮ __price_description__ `t: string`     описание цен предложенных вариантов
*    __notification_message__ `t: string`     текст сообщения

### requirements_request
   `t: object`  `f: requirements_request`   требования к автомобилю (запрос)

### requirements_response
   `t: object`  `f: requirements_response`   требования к автомобилю (ответ)

### route_in_order
   `t: array`     маршрут заказа
*   ⋮ __response__ `t: route_point`     объект ответа целиком

### route_point
   `t: object`     ?
*   ⋮ __country__ `t: string`    `min-length: 1` страна
*   ⋮ __fullname__ `t: string`    `min-length: 1` полный адрес
*   ⋮ __geopoint__ `t: point`     точка
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __accepts_exact5__ `t: boolean`     принимает ли данная точка отложенные 5.0
*    __closest_station__ `t: string`     ближайшая станция метро
*    __description__ `t: string`     мелко-подробности
*    __exact__ `t: boolean`     точно ли определен адрес
*    __flight__ `t: string`    `min-length: 1` рейс (для заказов в аэропорт)
*    __locality__ `t: string`     населенный пункт
*    __object_type__ `t: string` `v: аэропорт/организация/другое`    классификация объекта или организации
*    __oid__ `t: string`     идентификатор объекта
*    __porchnumber__ `t: string`     подъезд
*    __premisenumber__ `t: string`     дом
*    __short_text__ `t: string`     короткий адрес
*    __short_text_from__ `t: string`     короткий адрес после предлога ОТ (откуда)
*    __short_text_to__ `t: string`     короткий адрес после предлога ДО (куда)
*    __terminal__ `t: string`    `min-length: 1` терминал (для заказов в аэропорт)
*    __thoroughfare__ `t: string`     улица
*    __type__ `t: string` `v: address/organization`    тип объекта - адрес или организация
*    __use_geopoint__ `t: boolean`     при подаче следует использовать координаты, а не адрес

### routestats_service_levels
   `t: array`     положения селектора дёшево-комфортно
*   ⋮ __cars__ `t: array`     список автомобилей на заказ (не хуже)
*   ⋮ __class__ `t: tariff_class`     категория тарифа
    *   ⋮ __response__ `t: tariff_class`     объект ответа целиком
*   ⋮ __name__ `t: string`    `min-length: 1` название интервала
*   ⋮ __service_level__ `t: service_level`     идентификатор положения (передаётся в order)
    *   ⋮ __response__ `t: service_level`     объект ответа целиком
*    __description__ `t: string`     текстовое описание ориентировочной стоимости поездки
*    __description_markup__ `t: string`     Разметка текстового описания ориентировочной стоимости поездки
*    __description_parts__ `t: object`     разбитая на части строка description
    *    __prefix__ `t: string`     ?
    *    __suffix__ `t: string`     ?
    *    __value__ `t: string`     ?
*    __details__ `t: array`     описание составляющих стоимости поездки
    *   ⋮ __description__ `t: string`     описание составляющей
    *   ⋮ __price__ `t: string`     ориентировочная стоимость составляющей
*    __details_tariff__ `t: array`     описание составляющих минимального тарифа
    *   ⋮ __type__ `t: string` `v: price/icon/comment`    тип составляющей
    *   ⋮ __value__ `t: string`     локализованное значение составляющей
*    __estimated_waiting__ `t: object`     оценочное время ожидание машины с данным service_level
    *   ⋮ __message__ `t: string`     форматированная строка с ожидаемым временем
    *   ⋮ __seconds__ `t: number`     ожидаемое время в секундах
*    __forced_surge__ `t: object`     данные принудительного суржа
    *   ⋮ __comment__ `t: string`     комментарий по ожиданию окончания суржа
    *   ⋮ __description__ `t: string`     описание тарифа с суржем
    *   ⋮ __order_comment__ `t: string`     комментарий при создании заказа
    *   ⋮ __reason__ `t: string`     комментарий по причине увеличению суржа
    *   ⋮ __title__ `t: string`     текстовое описание величины суржа
    *   ⋮ __value__ `t: number`     величина суржа
    *    __color_button__ `t: boolean`     красить кнопку
    *    __hide_value__ `t: boolean`     не показывать пользователю коэффициент суржа
    *    __show_popup__ `t: boolean`     показать попап
    *    __title_card__ `t: string`     коэффициент суржа для карточек
*    __price__ `t: string`     ориентировочная стоимость поездки
*    __price_ride__ `t: string`     ориентировочная стоимость поездки (без учета купона)
*    __requirements__ `t: object`     необходимые ограничения
    *    __destination__ `t: boolean`     просить пользователя указать точку назначения
*    __show_description__ `t: boolean`     Если false не показывать description под title-ом кнопки
*    __tariff_unavailable__ `t: tariff_unavailable_message`     информация о причине недоступности тарифа
    *   ⋮ __response__ `t: tariff_unavailable_message`     объект ответа целиком
*    __title__ `t: string`     Заголовок кнопки
*    __title_markup__ `t: string`     Разметка заголовока кнопки

### schedule
   `t: object`     расписание действия временного интервала
*    __(1|2|3|4|5|6|7|holiday)__ `t: array`     расписание в заданный день недели или праздничный день
    *    __end__ `t: string`   `r: ([01][0-9]|2[0-3]):[0-5][0-9]`  окончание действия интервала, включительно
    *    __start__ `t: string`   `r: ([01][0-9]|2[0-3]):[0-5][0-9]`  начало действия интервала, включительно

### service_level
   `t: integer`     положение ползунка на шкале дёшево-комфортно

### supported_feedback_choices
   `t: `     Варианты фидбека в этом городе

### supported_requirements
   `t: array`     требования к заказу, регулируемые на стороне сервера
*   ⋮ __label__ `t: string`     Локализованное название для UI
*   ⋮ __name__ `t: string`     Внутреннее название требования
*   ⋮ __persistent__ `t: boolean`     Должен ли выбор пользователя сохраняться на стороне клиента
*   ⋮ __type__ `t: string` `v: boolean/select`    Тип требования
*    __description__ `t: string`     развернутое описание пожелания
*    __max_weight__ `t: number`     максимальный суммарный вес опций
*    __select__ `t: object`     Варианты вложенного выбора
    *   ⋮ __options__ `t: array`     ?
        *   ⋮ __label__ `t: string`     Локализованное название для UI
        *   ⋮ __name__ `t: string`     Внутреннее название вложенного требования
        *   ⋮ __value__ `t: string/number`     Значение варианта выбора
        *    __independent_tariffication__ `t: boolean`     тарифицировать ли опцию отдельно
        *    __max_count__ `t: integer`     максимальное количество
        *    __title__ `t: string`     Локализованный заголовок для UI
        *    __title_forms__ `t: object`     формы title для разного количества от 1 до max_count
        *    __weight__ `t: number`     условный вес опции
    *   ⋮ __type__ `t: string` `v: number/string`    Тип вложенного требования
    *    __caption__ `t: string`     Локализованный заголовок экрана выбора

### surge
   `t: object`     диалог сурж-прайсинга
*   ⋮ __decision_id__ `t: string`     id, который нужно отправить в ручку reorder
*    __button_label__ `t: string`     текст на кнопке подтверждения на диалоге сурж-прайсинга
*    __info__ `t: string`     полное описание предложения
*    __small_icon_label__ `t: string`     заголовок кнопки открытия диалога
*    __title__ `t: string`     заголовок диалогового окна

### tariff_class
   `t: string`  `f: tariff_class`   категория тарифа

### tariff_unavailable_message
   `t: object`     объект для сигнализации о том, что тариф недоступен
*   ⋮ __code__ `t: string`     код ошибки
*   ⋮ __message__ `t: string`     локализованный текст сообщения об ошибке

### time
   `t: number`     единица измерения времени

### tips
   `t: object`     чаевые
*   ⋮ __type__ `t: string` `v: percent`    единица измерения чаевых (percent - % от суммы заказа)
*   ⋮ __value__ `t: number`     размер чаевых (в единицах, указанных в поле type)

### updated_requirements
   `t: array`     требования, измененные в процессе заказа
*   ⋮ __reason__ `t: object`     причина изменения
    *   ⋮ __code__ `t: string` `v: NEED_CVN/ORDER_CANCELLED/ORDER_EXPIRED/UNUSABLE_CARD/INVALID_CARD/INITIATED_BY_USER`    код ошибки
    *    __text__ `t: string`     человекопонятное описание ошибки
*   ⋮ __requirement__ `t: string` `v: creditcard`    требование, у которого изменилось значение
*   ⋮ __value__ `t: boolean`     новое значение требования

### user_action
   `t: string` `v: user_ready`    действие пользователя

### user_feedback
   `t: object`     фидбэк пользователя на заказ
*    __call_me__ `t: boolean`     клиент попросил связаться с ним
*    __choices__ `t: feedback_choices`     варианты, которые выбрал пользователь
    *   ⋮ __response__ `t: feedback_choices`     объект ответа целиком
*    __msg__ `t: string`     текст комментария
*    __rating__ `t: feedback_rating`     оценка
    *   ⋮ __response__ `t: feedback_rating`     объект ответа целиком

### user_tips
   `t: object`     чаевые, переданные пользователем на заказ (могут быть изменены в зависимости от состояния заказа)
*   ⋮ __type__ `t: string` `v: percent`    единица измерения чаевых (percent - % от суммы заказа)
*   ⋮ __value__ `t: number`     размер чаевых (в единицах, указанных в поле type)
*    __available__ `t: boolean`     ?

### uuid4
   `t: string`   `r: ^[a-z0-9]{32}$`  уникальный буквенно-цифровой идентификатор длиной 32 символа

<a name="request_add_user_message"></a>
## add_user_message
### Описание

Ручка для добавления сообщений пользователя в чат.

В запрос приходит идентификатор авторизованного пользователя и сообщение.
Ручка доступна только для авторизованного пользователя. В ручку передаётся уникальный идентификтор сообщения,
который должен использоваться, если фронтенд хочет повторить отправку сообщения. Если сообщение с переданным идентификатором уже записано на бэкенд, то ответ будет с кодом 409.

### Пример

    {
        "id": "1234567890abcdefghijkl0987654321", # Идентификатор пользователя
        "message_id": "1234567890abcdefghijkl0123456789", # Идентификатор сообщения
        "message": "Текст сообщения",
        "type": "text"
    }

-

    {}

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __message__ `t: string`     сообщение
*   ⋮ __message_id__ `t: uuid4`     идентификатор сообщения
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __type__ `t: string`     тип сообщения

### Допустимые параметры ответа


<a name="request_allcars"></a>
## allcars
### Описание

Местоположение машин на карте города.

### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "br": [
            30.455555419677722,
            60.020072744833961
        ],
        "city": "Санкт-Петербург",
        "limit": 200,
        "tl": [
            30.300373534912097,
            60.076475774266711
        ]
    }

-

    [
        {
            "parkid": "000111",
            "cars": [
                {
                    "geopoint": [
                        30.336521999999999,
                        60.04092
                    ],
                    "uuid": "123654",
                    "free": true
                },
                {
                    "geopoint": [
                        30.334160000000001,
                        60.041873000000002
                    ],
                    "uuid": "asd123",
                    "free": false
                }
            ]
        },
        {
            "parkid": "000222",
            "cars": [
                {
                    "geopoint": [
                        30.3978,
                        60.039099999999998
                    ],
                    "uuid": "12984",
                    "free": false
                }
            ]
        }
    ]

### Допустимые параметры запроса

*   ⋮ __city__ `t: city`     город
    *   ⋮ __response__ `t: city`     объект ответа целиком
*    __br__ `t: point`     нижний правый угол области, в которой нужно показать машины
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __class__ `t: class`     класс автомобилей
    *   ⋮ __response__ `t: class`     объект ответа целиком
*    __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __limit__ `t: integer`     ограничение сверху количества возвращаемых машин
*    __parks__ `t: excluded_parks`     исключённые таксопарки
    *   ⋮ __response__ `t: excluded_parks`     объект ответа целиком
*    __tl__ `t: point`     верхний левый угол области, в которой нужно показать машины
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __zoom__ `t: integer`     зум карты, для которого нужно показать машины

### Допустимые параметры ответа

*   ⋮ __cars__ `t: array`     машины таксопарка
    *   ⋮ __free__ `t: boolean`     свободен ли водитель
    *   ⋮ __geopoint__ `t: point`     точка, в которой находится машина
        *   ⋮ __response__ `t: point`     объект ответа целиком
    *   ⋮ __uuid__ `t: string`    `min-length: 1` идентификатор машины (уникален в пределах таксопарка)
*   ⋮ __parkid__ `t: string`    `min-length: 6` идентификатор таксопарка

<a name="request_auth"></a>
## auth
### Описание

Функциональное назначение:

1.  запуск процедуры авторизации телефонного номера
2.  изменение телефонного номера у уже авторизованного пользователя
3.  изменение имени ранее авторизованного пользователя

При попытке авторизации (если пользователь ранее не был авторизован, или же если хочет изменить телефонный номер) пользователь получит смс с кодом подтверждения, который затем нужно передать в запрос `authconfirm`. До этого момента пользователь будет считаться неавторизованным и не сможет делать заказы.

Запрос на изменение имени ранее авторизованного пользователя не отличается от запросов на авторизацию: в запросе присутствуют всё те же `id` и `phone` и новое имя `name`. При успешном изменении имени сервер вёрнёт ответ `200 OK` с телом `{}`.

Код подтверждения всегда состоит из трех цифр.

### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "name": "Василий",
        "phone": "+71231231231"
    }

-

    {
        "authorized": true
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __phone__ `t: phone`     номер телефона пользователя
    *   ⋮ __response__ `t: phone`     объект ответа целиком
*    __name__ `t: string`    `min-length: 1` имя пользователя

### Допустимые параметры ответа

*    __authorized__ `t: boolean`     пользователь уже авторизован, подтверждение не требуется

<a name="request_authconfirm"></a>
## authconfirm
### Описание

Завершение процедуры авторизации телефонного номера.

Если введенный пользователем код совпадет с тем, который отправлял сервер, то пользователь будет считаться авторизованным и сможет сделать заказ.

Код подтверждения всегда состоит из трех цифр.

### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "confirmation_code": "123"
    }

-

    {
        "authorized": true
    }

### Допустимые параметры запроса

*   ⋮ __confirmation_code__ `t: string`   `r: ^\d{3,6}$`  код подтверждения авторизации
*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __authorized__ `t: boolean`     пользователь успешно авторизован
*    __attempts_left__ `t: integer`     оставшееся количество попыток ввести код
*    __block_time__ `t: string`    `min-length: 1` время, на которое будет заблокирован пользователь за превышение количества попыток

<a name="request_cards"></a>
## cards
### Описание

Получение информации о возможности использования безналичного расчёта и
получение списка карт, доступных для оплаты заказов пользователя.

Oauth-токен в заголовке `Authorization: Bearer TOKEN` обязателен. Перед
запросом необходимо сходить в `launch` с тем же токеном, привязав номер
телефона к устройству.

Возможные ошибки и рекомендации по их интерпретации:

  * `406 Not Acceptable`, `UNKNOWN_USER`: пользователь неизвестен;
    необходимо предварительно сделать запрос в launch
  * `401 Unauthorized`, `INVALID_TOKEN`: токен инвалидирован; необходимо
    получить новый токен и сделать запрос в launch со обновлённым
    токеном
  * `406 Not Acceptable`, `MISSING_TOKEN`: токен не передан
  * `406 Not Acceptable`, незивестный код ошибки; рекомендуется
    отобразить сообщение об ошибке пользователю (поле `error.text`) и
    вернуться на главный экран

### Пример

    {
        "id": "1234567890abcdefghijkl0987654321"
    }

-

    {
        "payment_available": true,
        "available_cards": [
            {
                "id": "card-123456789",
                "system": "VISA",
                "number": "4019******1234",
                "currency": "RUB",
                "busy": false,
                "usable": true
            }
        ]
    }

### Допустимые параметры запроса

*    __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __available_cards__ `t: array`     ?
    *   ⋮ __busy__ `t: boolean`     карта не может быть удалена
    *   ⋮ __currency__ `t: string`     валюта счета карты
    *   ⋮ __id__ `t: string`     id способа оплаты для передачи в заказ
    *   ⋮ __number__ `t: string`     номер карты (начало замаскировано звездочками)
    *   ⋮ __system__ `t: string`     платежная система карты (VISA, MasterCard)
    *   ⋮ __usable__ `t: boolean`     карта может быть использована для заказа с безналичным расчётом
*   ⋮ __payment_available__ `t: boolean`     данный вид оплаты доступен

<a name="request_changeaction"></a>
## changeaction
### Описание

Метод `/changeaction` позволяет передать серверу уведомление о действии,
которое совершил пользователь. Действие передается в поле `"action"`.

Поддерживаются действия:

|Действие|Описание|
|--------|--------|
|user_ready| Пользователь нажал на кнопку "Уже выхожу". Применимо только в *driving* или *waiting*|


### Заголовки
Сервер вернет заголовок Last-Orders-Modified
(в формате '2015-11-27T13:21:16.662842'). Как его использовать - см.
('/changes')[changes.md]

Клиент передает в поле `"created_time"` время (синхронизированное с
сервером) создания изменения.

В ответе в поле `"change_id"` сервер вернет уникальный идентификатор изменения.
По этому идентификатору клиент может следить за статусом изменения.
В поле "status" возвращается текущий статус изменения: "pending|failed|success".

Если сервер вернул 200, значит изменение было сохранено сервером, и волноваться
не нужно.

А вот если ...

### Коды ошибок

##### 404
Заказ с переданным *orderid* не был найден.

##### 406
Действие не может быть применено.

##### 409
Было применено кем-то (клиентом или водителем) с более поздним `"created_time"`.


### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1234567890mnopqrstuvwx0987654321",
        "created_time": "2013-03-13T08:57:22+0000",
        "action": "user_ready"
    }

# TODO(aershov182): is it okay that we return "name": "user_ready" and "value":
# true instead of "name": "action", "value": "user_ready"
-

    {
        "change_id": "7116f3e79bc843a09ef13756b04d19dc",
        "status": "success",
        "name": "user_ready",
        "value": true
    }

### Допустимые параметры запроса

*   ⋮ __action__ `t: user_action`     действие пользователя
    *   ⋮ __response__ `t: user_action`     объект ответа целиком
*   ⋮ __created_time__ `t: string`  `f: date-time`   UTC-время создания изменения
*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __orderid__ `t: uuid4`     идентификатор заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __change_id__ `t: uuid4`     уникальный идентификатор изменения
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __name__ `t: string`     тип изменения
*   ⋮ __status__ `t: change_status`     статус изменения
    *   ⋮ __response__ `t: change_status`     объект ответа целиком
*   ⋮ __value__ `t: object`     значение изменения

<a name="request_changecomment"></a>
## changecomment
### Описание

Метод `/changecomment` позволяет изменить комментарий заказа. Комментарий
передается в поле `"comment"`

### Заголовки
Сервер вернет заголовок Last-Orders-Modified
(в формате '2015-11-27T13:21:16.662842'). Как его использовать - см.
('/changes')[changes.md]

Клиент передает в поле `"created_time"` время (синхронизированное с
сервером) создания изменения.

В ответе в поле `"change_id"` сервер вернет уникальный идентификатор изменения.
По этому идентификатору клиент может следить за статусом изменения.
В поле "status" возвращается текущий статус изменения: "pending|failed|success".

Если сервер вернул 200, значит изменение было сохранено сервером, и волноваться
не нужно.

А вот если ...

### Коды ошибок

##### 404
Заказ с переданным *orderid* не был найден.

##### 406
Действие не может быть применено.

##### 409
Комментарий уже был изменен клиентом (или водителем) с более поздним `"created_time"`.


### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1234567890mnopqrstuvwx0987654321",
        "created_time": "2013-03-13T08:57:22+0000",
        "comment": "some comment"
    }

-

    {
        "change_id": "7116f3e79bc843a09ef13756b04d19dc",
        "status": "success"
        "name": "comment",
        "value": "some comment"
    }

### Допустимые параметры запроса

*   ⋮ __comment__ `t: string`     новый комментарий к заказу
*   ⋮ __created_time__ `t: string`  `f: date-time`   UTC-время создания изменения
*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __orderid__ `t: uuid4`     идентификатор заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __change_id__ `t: uuid4`     уникальный идентификатор изменения
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __name__ `t: string`     тип изменения
*   ⋮ __status__ `t: change_status`     статус изменения
    *   ⋮ __response__ `t: change_status`     объект ответа целиком
*   ⋮ __value__ `t: string`     значение изменения

<a name="request_changecorpcostcenter"></a>
## changecorpcostcenter
### Описание

Метод `/changecorpcostcenter` позволяет изменить кост-центр корпоративного заказа.
Кост-центр передается в поле `"corp_cost_center"`

### Заголовки
Сервер вернет заголовок Last-Orders-Modified
(в формате '2015-11-27T13:21:16.662842'). Как его использовать - см.
('/changes')[changes.md]

Клиент передает в поле `"created_time"` время (синхронизированное с
сервером) создания изменения.

В ответе в поле `"change_id"` сервер вернет уникальный идентификатор изменения.
По этому идентификатору клиент может следить за статусом изменения.
В поле "status" возвращается текущий статус изменения: "pending|failed|success".

Если сервер вернул 200, значит изменение было сохранено сервером, и волноваться
не нужно.

А вот если ...

### Коды ошибок

##### 404
Заказ с переданным *orderid* не был найден.

##### 406
Действие не может быть применено.

##### 409
Кост-центр уже был изменен клиентом (или водителем) с более поздним `"created_time"`.


### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1234567890mnopqrstuvwx0987654321",
        "created_time": "2013-03-13T08:57:22+0000",
        "corp_cost_center": "some cost center"
    }

-

    {
        "change_id": "7116f3e79bc843a09ef13756b04d19dc",
        "status": "success"
        "name": "corp_cost_center",
        "value": "some cost center"
    }

### Допустимые параметры запроса

*   ⋮ __corp_cost_center__ `t: string`     новый кост-центр к заказу
*   ⋮ __created_time__ `t: string`  `f: date-time`   UTC-время создания изменения
*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __orderid__ `t: uuid4`     идентификатор заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __change_id__ `t: uuid4`     уникальный идентификатор изменения
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __name__ `t: string`     тип изменения
*   ⋮ __status__ `t: change_status`     статус изменения
    *   ⋮ __response__ `t: change_status`     объект ответа целиком
*   ⋮ __value__ `t: string`     значение изменения

<a name="request_changedestinations"></a>
## changedestinations
### Описание

Метод `/changedestinations` позволяет изменить пункт назначения. Пункт назначения
передается в поле `"destinations"`.

### Заголовки
Сервер вернет заголовок Last-Orders-Modified
(в формате '2015-11-27T13:21:16.662842'). Как его использовать - см.
('/changes')[changes.md]

Клиент передает в поле `"created_time"` время (синхронизированное с
сервером) создания изменения.

В ответе в поле `"change_id"` сервер вернет уникальный идентификатор изменения.
По этому идентификатору клиент может следить за статусом изменения.
В поле "status" возвращается текущий статус изменения: "pending|failed|success".

Если сервер вернул 200, значит изменение было сохранено сервером, и волноваться
не нужно.

А вот если ...

### Коды ошибок

##### 404
Заказ с переданным *orderid* не был найден.

##### 406
Действие не может быть применено.

##### 409
Пункт назначения уже был изменен клиентом (или водителем) с более поздним `"created_time"`.


### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1234567890mnopqrstuvwx0987654321",
        "created_time": "2013-03-13T08:57:22+0000",
        "destinations": [
            {
                "country": "Россия",
                "fullname": "Россия, Москва, 8 Марта, 4",
                "geopoint": [
                    33.1,
                    52.1
                ],
                "locality": "Москва",
                "porchnumber": "",
                "premisenumber": "4",
                "thoroughfare": "8 Марта"
            }
        ]
    }

-

    {
        "change_id": "7116f3e79bc843a09ef13756b04d19dc",
        "status": "success"
        "name": "comment"
        "value": [
             {
                 "country": "Россия",
                 "fullname": "Россия, Москва, 8 Марта, 4",
                 "geopoint": [
                     33.1,
                     52.1
                 ],
                 "locality": "Москва",
                 "porchnumber": "",
                 "premisenumber": "4",
                 "thoroughfare": "8 Марта"
             }
         ]
    }

### Допустимые параметры запроса

*   ⋮ __created_time__ `t: string`  `f: date-time`   UTC-время создания изменения
*   ⋮ __destinations__ `t: route_in_order`     точки маршрута (без точки А)
    *   ⋮ __response__ `t: route_in_order`     объект ответа целиком
*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __orderid__ `t: uuid4`     идентификатор заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __change_id__ `t: uuid4`     уникальный идентификатор изменения
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __name__ `t: string`     тип изменения
*   ⋮ __status__ `t: change_status`     статус изменения
    *   ⋮ __response__ `t: change_status`     объект ответа целиком
*   ⋮ __value__ `t: `     значение изменения

<a name="request_changepayment"></a>
## changepayment
### Описание

Метод `/changepayment` позволяет изменить способ оплаты.
Новый способ оплаты передается в поле `"payment_method_id"`. Тип нового 
способа оплаты передается в поле `"payment_method_type"`. 
Если тип не укзаан, то считаем, что это карта. 
В поле `"payment_method_id"` надо передать id карты.

Клиент передает в поле `"created_time"` время (синхронизированное с
сервером) создания изменения.

В необязательном поле `"tips"` клиент может передать значение чаевых. Формат
такой же, как и в `/3.0/order`.


В ответе в поле `"change_id"` сервер вернет уникальный идентификатор изменения.
По этому идентификатору клиент может следить за статусом изменения.
Подробности - в [описании метода `/changes`](changes.md).

Если сервер вернул 200, значит изменение было сохранено сервером, и волноваться
не нужно.

А вот если ...

### Коды ошибок

##### 404
Заказ с переданным *orderid* не был найден.

##### 406
* При попытке изменить способ оплаты с карты на карту или с карты на наличные.
* Если заказ уже завершен.

##### 409
Метод оплаты уже был изменен клиентом с более поздним `"created_time"`.


### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1234567890mnopqrstuvwx0987654321",
        "created_time": "2013-03-13T08:57:22+0000",
        "payment_method_id": "card-012345",
        "tips": {
           "type": "percent",
           "value": 5
        }
    }

-

    {
        "change_id": "7116f3e79bc843a09ef13756b04d19dc",
        "status": "pending",
        "name": "payment",
        "value": "card-012345"
    }

### Допустимые параметры запроса

*   ⋮ __created_time__ `t: string`  `f: date-time`   UTC-время создания изменения
*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __orderid__ `t: uuid4`     идентификатор заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __payment_method_id__ `t: string`  `f: payment_id`  `min-length: 6` способ метода оплаты
*    __payment_method_type__ `t: payment_method`     ?
    *   ⋮ __response__ `t: payment_method`     объект ответа целиком
*    __tips__ `t: tips`     чаевые
    *   ⋮ __response__ `t: tips`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __change_id__ `t: uuid4`     уникальный идентификатор изменения
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __name__ `t: string`     тип изменения
*   ⋮ __status__ `t: change_status`     статус изменения
    *   ⋮ __response__ `t: change_status`     объект ответа целиком
*   ⋮ __value__ `t: string`     значение изменения

<a name="request_changeporchnumber"></a>
## changeporchnumber
### Описание

Метод `/changeporchnumber` позволяет изменить номер подъезда. Номер подъезда
передается в поле `"porchnumber"`

### Заголовки
Сервер вернет заголовок Last-Orders-Modified
(в формате '2015-11-27T13:21:16.662842'). Как его использовать - см.
('/changes')[changes.md]

Клиент передает в поле `"created_time"` время (синхронизированное с
сервером) создания изменения.

В ответе в поле `"change_id"` сервер вернет уникальный идентификатор изменения.
По этому идентификатору клиент может следить за статусом изменения.
В поле "status" возвращается текущий статус изменения: "pending|failed|success".

Если сервер вернул 200, значит изменение было сохранено сервером, и волноваться
не нужно.

А вот если ...

### Коды ошибок

##### 404
Заказ с переданным *orderid* не был найден.

##### 406
Действие не может быть применено.

##### 409
Номер подъезда уже был изменен клиентом (или водителем) с более поздним `"created_time"`.


### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1234567890mnopqrstuvwx0987654321",
        "created_time": "2013-03-13T08:57:22+0000",
        "porchnumber": "3"
    }

-

    {
        "change_id": "7116f3e79bc843a09ef13756b04d19dc",
        "status": "success"
        "name": "porchnumber",
        "value": "3"
    }

### Допустимые параметры запроса

*   ⋮ __created_time__ `t: string`  `f: date-time`   UTC-время создания изменения
*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __orderid__ `t: uuid4`     идентификатор заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __porchnumber__ `t: string`     подъезд

### Допустимые параметры ответа

*   ⋮ __change_id__ `t: uuid4`     уникальный идентификатор изменения
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __name__ `t: string`     тип изменения
*   ⋮ __status__ `t: change_status`     статус изменения
    *   ⋮ __response__ `t: change_status`     объект ответа целиком
*   ⋮ __value__ `t: string`     значение изменения

<a name="request_changes"></a>
## changes
### Описание

Метод `/changes` позволяет клиенту следить за статусом выполнения изменений,
которые нельзя применить сразу. Например, метод оплаты нельзя изменить
мгновенно, потому что надо проверить карту и, возможно, дождаться выполнения
антифрода.


#### Заголовки
Клиент передает в запросе заголовок Last-Orders-Modified
(в формате '2015-11-27T13:21:16.662842').
Текущее значение
можно взять из серверного заголовка Last-Orders-Modified в `/change*` методах.

Сервер будет использовать значение Last-Orders-Modified, чтобы определить
ходить ли за данными в primary или secondary.

## Внимание: в рамках текущих изменений - передавать Last-Orders-Modified не обязательно. Это будет больше иметь смысл в контексте мультизаказа.


### Пример

    /3.0/changes
    Last-Orders-Modified: 2013-03-13T08:57:22.2342
    {
        "id": "1234567890abcdefghijkl0987654321",
        "orders": [
            {
                "orderid": "1234567890abcdefghijkl0987654321",
                "changes": [
                    {
                        "change_id": "7116f3e79bc843a09ef13756b04d19dc",
                    }
                ]
            }
        ]
    }

-
    Last-Orders-Modified: 2013-03-13T08:58:38.23234
    {
        "orders": [
            {
                "orderid": "1234567890abcdefghijkl0987654321",
                "changes": [
                    {
                        "change_id": "7116f3e79bc843a09ef13756b04d19dc",
                        "name": "comment",
                        "value": "some comment",
                        "status": "pending"
                    }
                ]
            }
        ]
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __orders__ `t: array`     заказы
    *   ⋮ __changes__ `t: array`     ?
    *   ⋮ __orderid__ `t: `     идентификатор заказа

### Допустимые параметры ответа

*   ⋮ __orders__ `t: array`     заказы
    *   ⋮ __changes__ `t: array`     ?
    *   ⋮ __orderid__ `t: `     идентификатор заказа

<a name="request_cities"></a>
## cities
### Описание

Список городов, в которых работает Яндекс.Такси.

В поле `city` каждого города находится идентификатор, который следует передавать в параметре `city` во всех остальных запросах, где это требуется.

В поле `exact_orders` возвращается флаг, определяющий, можно ли в данном городе делать заказы на конкретное время (TAXIBACKEND-2233).
Если он сброшен или отсутствует, то попытка создать такой заказ через ручку `order` вернет 406 с ошибкой INVALID_ORDER_TYPE.

**Примечание:** поля `short_text_from` и `short_text_to` в поле `hotspots` на данный момент возвращают именительный падеж.

### "Новые" требования

В поле `supported_requirements` возвращаются "новые" требования к заказу, управляемые с сервера. Поле представляет собой
массив объектов следующего вида:

    {
        "name": "внутреннее название (идентификатор) требование, например, nosmoking",
        "label": "человекочитаемое название (для UI), зависит от локали",
        "type": "boolean" или "select",
        "select": {
            "caption": "название экрана для выбора опций (для UI), может отсутствовать, зависит от локали",
            "type": "string" или "number",
            "options": [{
                "label": "человекочитаемое название опции (для UI), зависит от локали",
                "name": "внутреннее название (идентификатор) вложенной опции"
                "value": "значение, которое нужно передать на сервер",
            }, {...}]
        }
    }

Клиенты должны сохранять порядок требований в массиве при отображении на экране.

Тип требования определяется по полю `type`. Если оно равно `boolean`, требование считается флажком. Если клиент
активирует такое требование, в объект `requirements` в соответствующих ручках (`order`, `couponcheck`,
`routestats` и др.) должна добавляться пара `name: true`. Для неактивного требования пара не добавляется.

Если тип равен `select`, требование считается меню. При этом в нем должен присутствовать вложенный объект `select`.
Если клиент выбирает один из вариантов, предложенных в таком требовании, в объект `requirements` в соответствующих
ручках (`order`, `couponcheck`, `routestats` и др.) должна добавляться пара
`name: select.options.value`. Для неактивного требования пара не добавляется.
В случае, если поле `select.caption` отсутствует, заголовок экрана вложенного выбора считается равным `label`
требования.
 
Опции вложенного выбора (объект `select`) имеют свой тип, (очевидно) не совпадающий с типом требования. Им может быть
`string` (строка) или `number` (число).

ВАЖНО: клиент должен игнорировать (не отображать пользователю и не передавать на сервер) требования, тип которых
он не умеет обрабатывать.

Флаг `persistent` показывает, что выбор пользователем данного требования должен сохраняться на стороне клиента.
Например, если пользователь сделал выбор "некурящий водитель", и в данном городе требование "nosmoking" помечено
как `persistent`, клиент должен автоматически проставлять его во всех последующих заказах.

ВАЖНО: "старые" требования (`requirements`) оставлены для обратной совместимости и не предполагаются к использованию
в новых клиентах.

В `supported_requirements` приходят только те требования, которые должны быть отображены на соответствующем экране
клиентского приложения. "Псевдотребования" `coupon`, `creditcard` и `corp` теперь приходят в объекте `payment_options`.
Данный объект может отсутствовать; в этом случае считается, что в городе не доступны ни оплата купоном, ни оплата
картой, ни оплата корпоративной поездкой.


### Возможные причины отмены заказа или низкого рейтинга в городе
В поле `supported_feedback_choices` возвращается словарь с возможными вариантами 
причины отмены.

Поле `supported_feedback_choices` выглядит так:

    {
        "cancelled_reason": [choice_1, choice_2, ...],
    }

Каждый choice имеет вид:

    {
        "name": "внутреннее название (идентификатор) причины, например, driverrequest",
        "label": "человекочитаемое название (для UI), зависит от локали",
        "image_tag": "тэг изображения (для метода `getimage`), необязательное поле"
    }

Клиенты должны сохранять порядок причин в массиве при отображении на экране.
"name" причин можно передавать в метод `feedback` (во вложенное поле
 "cancelled_reason" в поле "choices").

### Правила обязательности точки Б

Создание заказов без конечной точки ("точки Б") может быть:

* отключено в городе как таковом. В этом случае в ответе ручки будет поле
    `req_destination`, установленное в значение `true` (текущее поведение).

* допустимо только для заказов, удовлетворяющих некоторым условиям. В этом
    случае в ответе будет поле `req_destination_rules`, описанное ниже.

Таким образом, `req_destination` и `req_destination_rules` являются взаимоисключающими.

Поле `req_destination_rules` - это объект, ключами которого являются условия
обязательности точки Б. В данный момент таким условием может быть только одно:

* `min_timedelta`, минимальное время до подачи машины (целое число, секунды).


### Пример

    {
        "id": "1234567890abcdefghijkl0987654321"
    }

-

    [{
        "hotspots": [{
            "city": "Москва",
            "description": "Москва, Россия",
            "full_text": "Россия, Московская область, Химки, аэропорт Шереметьево",
            "point": [37.414909999999999, 55.966732999999998],
            "house": "",
            "object_type": "аэропорт",
            "exact": true,
            "street": "аэропорт Шереметьево",
            "radius": 300,
            "country": "Россия",
            "short_text": "аэропорт Шереметьево",
            "short_text_from": "аэропорт Шереметьево",
            "short_text_to": "аэропорт Шереметьево",
            "type": "organization"
        }],
        "city": "Москва",
        "tl": [37.072422000000003, 55.999344000000001],
        "tz": "+0400",
        "tariff_calc": true,
        "br": [38.146335999999998, 55.395950999999997],
        "service_levels": [{
            "cars": ["Renault Logan", "Nissan Almera"],
            "service_level": 50,
            "name": "эконом"
        },
        {
            "cars": ["Kia Ceed", "Ford Mondeo"],
            "service_level": 70,
            "name": "комфорт"
        },
        {
            "cars": ["Mercedes E", "Mercedes S"],
            "service_level": 90,
            "name": "бизнес"
        }],
        "requirements": {
            "animaltransport": true,
            "universal": true,
            "coupon": true,
            "childchair": true,
            "check": true
        },
        "supported_requirements": [
            {
                "name": "animaltransport",
                "label": "Перевозка животных",
                "type": "boolean"
            },
            {
                "name": "universal",
                "label": "Кузов-универсал",
                "type": "boolean"
            },
            {
                 "name": "childchair",
                 "label": "Детское кресло",
                 "type": "select",
                 "select": {
                     "caption": "Тип кресла",
                     "type": string,
                     "options": [
                         {
                             "label": "Люлька",
                             "name": "cradle",
                             "value": "0-3",
                         },

                         {
                             "label": "Кресло",
                             "name": "chair",
                             "value": "3-7",
                         },

                         {
                             "label": "Бустер",
                             "name": "booster",
                             "value": "7-12",
                         }
                     ]
                 }
            },
        ],
        "supported_feedback_choices": {
            "cancelled_reason": [ 
                {
                    "name": "driverrequest",
                    "label": "Водитель попросил отменить"
                },
                {
                    "name": "usererror",
                    "label": "Заказал по ошибке"
                },
                {
                    "name": "longwait",
                    "label": "Слишком долго ждать"
                },
                {
                    "name": "othertaxi",
                    "label": "Уехал на другом такси"
                },
                {
                    "name": "droveaway",
                    "label": "Водитель ехал в другую сторону"
                }
            ]
        }
        "payment_options": {
            "coupon": true
        },
        "class": ["econom", "business", "vip"],
        "geo_id": 213,
        "max_tariffs_url": "https://m.taxi.yandex.ru/city-tariff/?city=%D0%9C%D0%BE%D1%81%D0%BA%D0%B2%D0%B0"
    },
    {
        "hotspots": [],
        "city": "Красноярск",
        "tl": [92.590192999999999, 56.198701999999997],
        "tz": "+0800",
        "br": [93.416915000000003, 55.927497000000002],
        "service_levels": [{
            "cars": ["Chevrolet Lacetti", "Renault Logan"],
            "service_level": 50,
            "name": "второй"
        },
        {
            "cars": ["Ford Focus", "Hyundai Solaris"],
            "service_level": 70,
            "name": "третий"
        },
        {
            "cars": ["Škoda Superb", "Ford Mondeo"],
            "service_level": 90,
            "name": "1й"
        }],
        "requirements": {},
        "supported_requirements": [],
        "supported_feedback_choices": {},
        "precalc_cost": true,
        "class": ["econom", "business", "vip"],
        "req_destination_rules": {
            "min_timedelta": 1500
        },
        "geo_id": 62
    },
    {
        "hotspots": [{
            "city": "Санкт-Петербург",
            "description": "Санкт-Петербург, Россия",
            "full_text": "Россия, Санкт-Петербург, аэропорт Пулково, терминал 1",
            "point": [30.269110000000001, 59.797891],
            "country": "Россия",
            "object_type": "аэропорт",
            "exact": true,
            "street": "аэропорт Пулково",
            "radius": 300,
            "house": "",
            "short_text": "аэропорт Пулково-1",
            "short_text_from": "аэропорт Пулково-1",
            "short_text_to": "аэропорт Пулково-1",
            "type": "organization"
        }],
        "precalc_cost": true,
        "br": [31.159165000000002, 59.536133999999997],
        "service_levels": [{
            "cars": ["Daewoo Nexia", "Renault Logan"],
            "service_level": 0,
            "name": "дешевле"
        },
        {
            "cars": ["Nissan Almera", "Chevrolet Lacetti"],
            "service_level": 50,
            "name": "оптимально"
        },
        {
            "cars": ["Ford Focus", "Ford Mondeo"],
            "service_level": 100,
            "name": "комфортнее"
        }],
        "requirements": {
            "animaltransport": true,
            "universal": true,
            "childchair": true,
            "check": true,
        },
        "supported_requirements": [],
        "supported_feedback_choices": {},
        "class": ["econom", "business", "vip"],
        "city": "Санкт-Петербург",
        "tz": "+0400",
        "geo_id": 2,
        "tl": [29.481003000000001, 60.280983999999997],
        "req_destination": true,
        "exact_orders": true
    }]

### Допустимые параметры запроса

*    __format_currency__ `t: boolean`      если передан, то в ответе передаем валюты в определенном формате
*    __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __supports_no_cars_available__ `t: boolean`     данные о поддержке клиентом ответа no_cars_available

### Допустимые параметры ответа

*   ⋮ __br__ `t: point`     нижний правый угол области, накрывающей город
    *   ⋮ __response__ `t: point`     объект ответа целиком
*   ⋮ __city__ `t: string`     название города на русском языке
*   ⋮ __service_levels__ `t: array`     положения селектора дёшево-комфортно
    *   ⋮ __cars__ `t: array`     список автомобилей на заказ (не хуже)
    *   ⋮ __name__ `t: string`    `min-length: 1` название интервала
    *   ⋮ __service_level__ `t: service_level`     идентификатор положения (передаётся в order)
        *   ⋮ __response__ `t: service_level`     объект ответа целиком
    *    __can_be_default__ `t: boolean`     этот тариф может быть заполнен в качестве тарифа по умолчанию
    *    __only_for_soon_orders__ `t: boolean`     по этому заказу можно делать только soon-заказы
    *    __restrict_by_payment_type__ `t: array`     поддерживаемые типы оплаты для данного тарифа (отсутствие поля означает поддержку всех типов)
        *   ⋮ __response__ `t: payment_method`     объект ответа целиком
*   ⋮ __tl__ `t: point`     верхний левый угол области, накрывающей город
    *   ⋮ __response__ `t: point`     объект ответа целиком
*   ⋮ __tz__ `t: string`   `r: ^(\+|-|)\d{2}(\:?\d{2})?$`  таймзона города
*    __class__ `t: class`     список категорий тарифов, поддерживаемых таксопарками данного города
    *   ⋮ __response__ `t: class`     объект ответа целиком
*    __currency_rules__ `t: currency_rules`     данные о валюте заказа (если клиент запросил)
    *   ⋮ __response__ `t: currency_rules`     объект ответа целиком
*    __exact_orders__ `t: boolean`     допускается ли делать заказы на конкретное время
*    __geo_id__ `t: integer`     идетификатор города из геобазы
*    __hotspots__ `t: array`     наиболее популярные места заказа такси в городе
    *   ⋮ __city__ `t: string`     город
    *   ⋮ __country__ `t: string`     страна
    *   ⋮ __exact__ `t: boolean`     точная ли информация о месте(для hotspots всегда true)
    *   ⋮ __full_text__ `t: string`     полный адрес
    *   ⋮ __house__ `t: string`     дом
    *   ⋮ __object_type__ `t: string` `v: аэропорт/другое`    классификация объекта или организации
    *   ⋮ __point__ `t: point`     координаты объекта или организации
        *   ⋮ __response__ `t: point`     объект ответа целиком
    *   ⋮ __radius__ `t: integer`     радиус притяжения
    *   ⋮ __short_text__ `t: string`     короткий адрес
    *   ⋮ __street__ `t: string`     улица
    *   ⋮ __type__ `t: string` `v: address/organization`    тип объекта - адрес или организация
    *    __description__ `t: string`     мелко-подробности
    *    __oid__ `t: string`     идентификатор объекта
    *    __short_text_from__ `t: string`     короткий адрес после предлога ОТ (откуда)
    *    __short_text_to__ `t: string`     короткий адрес после предлога ДО (куда)
*    __max_tariffs_url__ `t: string`     ссылка на описание МРТ на сайте
*    __payment_options__ `t: object`     возможные опции, влияющие на оплату заказа
    *    __coupon__ `t: boolean`     доступна оплата промокодом
    *    __creditcard__ `t: boolean`     доступна оплата по кредитной карте
*    __precalc_cost__ `t: boolean`     в этом городе работает предварительный расчет стоимости поездки
*    __req_destination__ `t: boolean`     при заказе в этом городе обязательно указывать точку назначения
*    __requirements__ `t: requirements_response`     требования, которые можно указывать при заказе в этом городе
    *   ⋮ __response__ `t: requirements_response`     объект ответа целиком
*    __support_phone__ `t: phone`     телефон службы поддержки в данном городе
    *   ⋮ __response__ `t: phone`     объект ответа целиком
*    __supported_feedback_choices__ `t: supported_feedback_choices`     возможные варианты фидбэка в этом городе
    *   ⋮ __response__ `t: supported_feedback_choices`     объект ответа целиком
*    __supported_requirements__ `t: supported_requirements`     требования, которые можно указывать при заказе в этом городе (новый формат)
    *   ⋮ __response__ `t: supported_requirements`     объект ответа целиком
*    __tariff_calc__ `t: boolean`     в этом городе работает калькулятор тарифов

<a name="request_couponcheck"></a>
## couponcheck
### Описание

Запрос для проверки промокода (ранее - купона).

Обязательными параметрами являются `id` — идентификатор пользователя и `city` — город, в котором предполагается использовать промокод. На данный момент промокоды действуют только в Москве.

Код промокод передается одним из следующих способов::

1. напрямую в параметре `coupon`;
2. в данных о заказе; в этом случае обязательным является только `requirements`, в котором, в свою очередь, обязательным является только ключ `coupon` (наличие или отсутствие других параметров заказа несущественно).

В случае, если карта выбрана способом оплаты по умолчанию, клиент должен передавать идентификатор карты в объекте `payment`, имеющем ту же структуру, что и в ручке `order`.

Код промокода может быть:
1. цифровым (12 цифр, из которых первые две цифры - код серии, последняя цифра - контрольный код);
1. цифробуквенным (кириллица, латиница и цифры), длина от 6 до 20 символов.

Если нет ни того, ни другого параметра, возвращается ошибка 400.
Если пользователь не авторизован, возращается ошибка 401, если заблокирован - 403.
Если пользователь выполняет данный запрос чаще, чем 5 раз за 3 минуты, возвращается ошибка 423 (при этом запросы, на которые вернулась ошибка 400, в этом числе не учитываются).

В остальных случаях возвращается объект с несколькими ключами:

* `valid` - true/false (можно ли использовать данный промокод),
* `valid_any` - true/false. Может ли промокод с `valid: false` стать действительным в другой раз (в другом городе, в другое время, ...). Отсутствует для промокодов с `valid: true`.
* `descr` - текстовое описание промокода, если он найден, либо сообщение о неверном промокоде.
* `details` - массив строк, содержащих дополнительную информацию о промокоде (срок окончания действия, число оставшихся поездок и т.п.)

Язык сообщений в полях `descr` и `details` зависит от значения заголовка запроса `Accept-Language`. Массив `details` может быть пустым.


### Пример 1

    {
        "id": "1234567890abcdefghijkl0987654321",
        "coupon": "014444444443",
        "city": "Москва"
    }

-

    {
        "valid": true,
        "descr": "Cкидка 300 рублей на следующую поездку",
        "details": ["Истекает: 14.04.2015"]
    }


### Пример 2

    {
        "id": "1234567890abcdefghijkl0987654321",
        "coupon": "014444444444",
        "city": "Москва"
    }

-

    {
        "valid": false,
        "descr": "Неверный промокод",
        "details": []
    }


### Пример 3

    {
        "id": "1234567890abcdefghijkl0987654321",
        "city": "Москва",
        "class": [
            "econom"
        ],
        "parks": [
            "000111",
            "000112"
        ],
        "requirements": {
            "animaltransport": true,
            "coupon": "014444444443"
        },
        "route": [
            {
                "country": "Россия",
                "fullname": "Россия, Москва, Новосущевская, 1",
                "geopoint": [
                    33.6,
                    55.1
                ],
                "locality": "Москва",
                "porchnumber": "1",
                "premisenumber": "1",
                "thoroughfare": "Новосущевская"
            },
            {
                "country": "Россия",
                "fullname": "Россия, Москва, 8 Марта, 4",
                "geopoint": [
                    33.1,
                    52.1
                ],
                "locality": "Москва",
                "porchnumber": "",
                "premisenumber": "4",
                "thoroughfare": "8 Марта"
            }
        ],
        "due": "2013-04-01T14:00:00+0400"
    }

-

    {
        "valid": true,
        "descr": "Cкидка 300 рублей на следующую поездку",
        "details": ["Истекает: 14.04.2015"]
    }


### Пример 4

    {
        "id": "1234567890abcdefghijkl0987654321",
        "coupon": "014444444443",
        "city": "Москва",
        "payment": {
            "type": "card",
            "payment_method_id": "card-x666"
        }
    }

-

    {
        "valid": true,
        "descr": "Cкидка 300 рублей на следующую поездку",
        "details": ["Действует при оплате картой"]
    }


### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __city__ `t: city`     город
    *   ⋮ __response__ `t: city`     объект ответа целиком
*    __coupon__ `t: coupon_request`     код купона
    *   ⋮ __response__ `t: coupon_request`     объект ответа целиком
*    __format_currency__ `t: boolean`      если передан, то в ответе передаем валюты в определенном формате
*    __payment__ `t: payment`     данные по оплате
    *   ⋮ __response__ `t: payment`     объект ответа целиком
*    __requirements__ `t: object`     требования к автомобилю
    *    __coupon__ `t: boolean`     оплата купоном
*    __zone_name__ `t: string`     название зоны

### Допустимые параметры ответа

*   ⋮ __descr__ `t: string`     текстовое описание купона (например, «скидка 300 руб.»)
*   ⋮ __valid__ `t: boolean`     можно ли использовать данный купон
*    __currency_rules__ `t: currency_rules`     данные о валюте заказа (если клиент запросил)
    *   ⋮ __response__ `t: currency_rules`     объект ответа целиком
*    __details__ `t: array`     дополнительная информация (число оставшихся поездок, срок действия)
*    __valid_any__ `t: boolean`     может ли купон быть использован при других условиях (время, город, ...)

<a name="request_deptranscars"></a>
## deptranscars
### Описание

Ручка для Департамента Транспорта. Отдает данные по местонахождению активных водителей и их статусу.

Если передан правильный заголовок `Yandex-Api-Key`, то по водителям некоторых парков 
отдаются дополнительные сведения: номер разрешения Дептранса, госномер, модель автомобиля
и список парков (из числа разрешенных), в которых работает данный госномер.

### Пример ответа без заголовка Yandex-Api-Key

    {
    }

-

    [
        {
            "geopoint": [
                30.336521999999999,
                60.04092
            ],
            "free": true
        },
        {
            "geopoint": [
                30.334160000000001,
                60.041873000000002
            ],
            "free": false
        }
    ]


### Пример ответа с заголовком Yandex-Api-Key

    {
    }

-

    [
        {
            "geopoint": [
                30.336521999999999,
                60.04092
            ],
            "id": "34fa2dcac7b8abf3ec5eb1e5e6036288",
            "free": true
        },
        {
            "geopoint": [
                30.334160000000001,
                60.041873000000002
            ],
            "free": false,
            "car_number": "A666СС77",
            "parks": ["Park Number One", 'Park Number Two"],
            "permit": "54321",
            "model": "Skoda Octavia"
        },
    ]

### Допустимые параметры запроса


### Допустимые параметры ответа

*   ⋮ __free__ `t: boolean`     свободен ли водитель
*   ⋮ __geopoint__ `t: point`     точка, в которой находится машина
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __car_number__ `t: string`     госномер автомобиля (только для разрешенных парков)
*    __id__ `t: string`     суррогатный id машины
*    __model__ `t: string`     модель автомобиля (только для разрешенных парков)
*    __parks__ `t: array`     парки, где работает данный госномер (только разрешенные)
*    __permit__ `t: string`     номер разрешения Дептранса (только для разрешенных парков)

<a name="request_email"></a>
## email
### Описание

Управление адресом электронной почты пользователя.

В текущей версии возможно создать, изменить или удалить один адрес
электронной почты на одно пользователькое устройство. При изменении
адреса или добавлении нового требуется подтверждение - бекенд высылает
письмо с секретным кодом, который нужно передать обратно в ручку.

Ручка доступна только для авторизованных пользователей. Исключение составляют
действия `confirm_email` и `unset`, в которых допускается альтернативная
"авторизация" через `confirmation_code`. Это необходимо, поскольку данные
действия могут косвенно вызываться через ссылки в отправленном пользователе письме,
где мы не хотим светить `user_phone_id`.

Общий формат запроса к ручке `email`:

    {
        "id": "идентификатор пользователя",
        "action": "действие",
        ...параметры действия...
    }

Общий формат ответа:

    {
        "status": "актуальный статус адреса электронной почты"
        ...дополнительные параметры...
    }
    
Для ответов с ошибочным кодом (4xx) тело может быть пустым.

Возможные статусы:

* `ok`: все в порядке (последнее действие выполнено успешно,
    адрес подтвержден и т.п.)

* `confirmation_sent`: для адреса выслано подтверждение
    (ипользуется в действии `set`)

* `confirmation_error`: подтверждение адреса завершилось с ошибкой
    (используется в действии `confirm`)
    
* `not_confirmed`: адрес не подтвержден (используется в действии `get`,
    поскольку неподтвержденность адреса для него не является ошибкой)

Возможные действия (`action`) и их параметры:

* `set`: установить (добавить или изменить) адрес электронной почты
    для данного `id`. Если с `id` ранее не был связан адрес электронной
    почты, выполняется добавление, иначе - изменение.
    
    Дополнительные параметры запроса: `email` (адрес).
    
    Параметры ответа: `status` (`ok` или `confirmation_sent`). В случае,
    если запрос происходит слишком часто, будет возвращен код 429 с пустым
    телом.

* `unset`: удалить адрес электронной почты (отписаться) для данного `id` или
    `confirmation_code`
 
    Дополнительные параметры запроса: `confirmation_code` (при отсутствии `id`).
    
    Параметры ответа: `status` (`ok`) или 404 с пустым телом, если данный
    `id`/`confirmation_code` не имеет привязанных адресов.
    
* `get`: получить текущий адрес электронной почты для данного `id`.

    Дополнительные параметры запроса: нет.
    
    Параметры ответа: `status` (`ok` или `not_confirmed`), `email`, либо
        404 с пустым телом, если данный `id` не имеет привязанных адресов.
    
* `confirm`: подтвердить адрес электронной почты.

    Дополнительные параметры запроса: `email` (адрес электронной почты),
        `confirmation_code` (секретный код). Обратите внимание:
        `id` в этом случае не передается.
        
    Параметры ответа: код 200 со `{"status": "ok"}`, если подтвержден;
        код 406 со `{"status": "confirmation_error"}`, если
        `confirmation_code` или `email` заданы некорректно.
        
Любые другие действия, а также неверно заданные или отсутствующие параметры,
приводят к коду 400 с пустым телом ответа. Отсутствие `id` или
`confirmation_code` в соответствующих действиях приводит к коду ответа 401
с пустым телом. В случае, если ручка требует наличия `id`, подразумевается,
что пользователь должен быть авторизован, иначе также вернется 401
с пустым телом.

    
### Примеры

Привязка нового адреса:

    {
        "id": "1234567890abcdefghijkl0987654321",
        "action": "set",
        "email": "my@mail.ru"
    }

-

    {
        "status": "confirmation_sent"
    }
    
Получение текущего привязанного адреса:
    
    {
        "id": "1234567890abcdefghijkl0987654321",
        "action": "get"
    }
    
-
    {
        "status": "not_confirmed",
        "email": "my@mail.ru"
    }
    
Подтверждение адреса электронной почты:

    {
        "action": "confirm",
        "email": "my@mail.ru",
        "confirmation_code": "dd8acc84e8cb80470782b755c4983f249838f2bf7dace7d1c078e5c2"
    }
    
-
    {
        "status": "ok"
    }
    
Удаление привязанного адреса электронной почты:
    
    {
        "id": "1234567890abcdefghijkl0987654321",
        "action": "unset"
    }
    
-

    {
        "status": "ok"
    }

То же самое, но с "авторизацией" по confirmation_code:

    {
        "confirmation_code": "dd8acc84e8cb80470782b755c4983f249838f2bf7dace7d1c078e5c2",
        "action": "unset"
    }
    
-

    {
        "status": "ok"
    }

### Допустимые параметры запроса

*  Вариант 1
    *   ⋮ __action__ `t: string` `v: set`    требуемое действие
    *   ⋮ __email__ `t: email`     адрес электронной почты
        *   ⋮ __response__ `t: email`     объект ответа целиком
    *   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
        *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*  Вариант 2
    *   ⋮ __action__ `t: string` `v: get`    требуемое действие
    *   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
        *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*  Вариант 3
    *    __action__ `t: string` `v: unset`    требуемое действие
    *    __confirmation_code__ `t: string`     код подтверждения
    *    __id__ `t: uuid4`     идентификатор сессии пользователя
        *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*  Вариант 4
    *   ⋮ __action__ `t: string` `v: confirm`    требуемое действие
    *   ⋮ __confirmation_code__ `t: string`     код подтверждения
    *   ⋮ __email__ `t: email`     адрес электронной почты
        *   ⋮ __response__ `t: email`     объект ответа целиком

### Допустимые параметры ответа

*    __email__ `t: email`     адрес электронной почты
    *   ⋮ __response__ `t: email`     объект ответа целиком
*    __status__ `t: email_status`     текущий статус адреса электронной почты
    *   ⋮ __response__ `t: email_status`     объект ответа целиком

<a name="request_feedback"></a>
## feedback
### Описание

Оценка и отзыв пользователя о заказе.

Пользователь может оставить оценку по пятибалльной шкале, текстовый отзыв или и то, и другое. Для одного и того же заказа запрос можно делать неограниченное количество раз, но будет сохранен только самый последний отзыв. Если в запросе нет ни оценки, ни текстового отзыва, сервер все равно больше не будет предлагать оценивать этот заказ.

Сервер позволяет оценить любой заказ пользователя, в том числе отмененный самим пользователем. При этом для отмененных пользователем заказов будет сохранен текстовый отзыв, а оценка может как сохраняться, так и не сохраняться в зависимости от настроек системы защиты от накруток рейтинга на сервере.

Также клиент по желанию может установить размер чаевых.

Дополнительно клиент может передать просьбу "Прошу связаться со мной"
(поле `call_me`).

Клиент может передать время генерации фидбэка (поле `created_time`).
Это поле нужно передавать если фидбэк менялся/меняется во время поездки.
Если сервер уже сохранил фидбэк с более поздним created_time, чем переданный
клиентом, то сервер вернет 409 и не сохранит фидбэк.

### Поле choices
В поле choices можно передать предопределенные варианты выбора. 
Например, причины отмены или причины низкого рейтинга.

В общем случае поле `choices` выглядит так:
{
    "choice_type_1": [choice_1, choice_2, ...],
    "choice_type_2": [choice_a, choice_b, ...],
    ...
}
Для choice_type == "low_rating_reason" choice надо брать из метода `taxiontheway`
(поле supported_feedback_choices).

Для choice_type == "cancelled_reason" choice надо брать из метода `cities`
(поле supported_feedback_choices).

Если пара (choice_type, choice) не поддерживается в городе, в котором был сделан заказ,
то feedback вернет 404.

Если в choices есть ключ "cancelled_reason", а заказ не был отменен пользователем, то
feedback вернет 400.


### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1234567890mnopqrstuvwx0987654321",
        "rating": 5,
        "tips": {
            "type": "percent",
            "value": 25
        },
        "choices": {
            "cancelled_reason": ["driverrequest"], 
            "low_rating_reason": ["rudedriver", "driverlate"]
        },
        "call_me": true,
        "created_time": "2013-04-01T14:00:00+0300"
    }

-

    {}

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __orderid__ `t: uuid4`     идентификатор заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __app_comment__ `t: boolean`     Флаг о том, что отзыв о приложении
*    __call_me__ `t: boolean`     Просьба связаться с пользователем
*    __choices__ `t: feedback_choices`     Варианты, которые выбрал пользователь
    *   ⋮ __response__ `t: feedback_choices`     объект ответа целиком
*    __created_time__ `t: string`  `f: date-time`   UTC-время создания изменения
*    __msg__ `t: string`     текст комментария
*    __rating__ `t: feedback_rating`     оценка
    *   ⋮ __response__ `t: feedback_rating`     объект ответа целиком
*    __tips__ `t: tips`     чаевые
    *   ⋮ __response__ `t: tips`     объект ответа целиком

### Допустимые параметры ответа


<a name="request_freecars"></a>
## freecars
### Описание

Местоположение свободных машин на карте города.

### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "city": "Санкт-Петербург",
        "class": [
            "econom",
            "business"
        ]
    }

-

    [
        [
            30.336521999999999,
            60.04092
        ],
        [
            30.334160000000001,
            60.041873000000002
        ],
        [
            30.3978,
            60.039099999999998
        ]
    ]

### Допустимые параметры запроса

*   ⋮ __city__ `t: city`     город
    *   ⋮ __response__ `t: city`     объект ответа целиком
*    __class__ `t: class`     класс автомобилей
    *   ⋮ __response__ `t: class`     объект ответа целиком
*    __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __parks__ `t: excluded_parks`     исключённые таксопарки
    *   ⋮ __response__ `t: excluded_parks`     объект ответа целиком
*    __requirements__ `t: requirements_request`     требования к автомобилю
    *   ⋮ __response__ `t: requirements_request`     объект ответа целиком
*    __service_level__ `t: service_level`     идентификатор положения на селекторе дешевле/удобнее
    *   ⋮ __response__ `t: service_level`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __response__ `t: point`     объект ответа целиком

<a name="request_geomagnet"></a>
## geomagnet
### Описание
"Притягивание" точки к координатам геообъекта с дополнительными параметрами (пока поддерживается номер подъезда).

## Коды ответа
* __404__: адрес или подъезд не найден на карте, притягивание выполнять не следует

### Допустимые параметры запроса

*   ⋮ __full_text__ `t: string`     название организации или полный адрес геообъекта
*    __ll__ `t: point`     текущее положение пина
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __porch_number__ `t: string`     номер подъезда

### Допустимые параметры ответа

*   ⋮ __response__ `t: address`     объект ответа целиком

<a name="request_geosearch"></a>
## geosearch
### Описание

Доступ к геопоиску и геокодированию Яндекс.Карт.

Три способа использования:

1.  Обратное геокодирование.

    В `what` передаются координаты объекта в виде массива `[(долгота), (широта)]`.

2.  Поиск объектов вблизи заданной точки.

    В `what` передаётся строка (например, "льва толстого 16"), в `ll` - координаты центра.

    Если значением параметра `sort` будет `dist` (по умолчанию), то найденные объекты будут отсортированы в порядке удаления от заданной в `ll` точки; если `uniform`, то сортировка в большей степени будет соответствовать релевантности объектов в соответсвии с переданным в `what` значением, чем переданным в `ll` координатам.

3.  Поиск объектов в рамках заданного окна.

    В `what` передаётся строка (например, "льва толстого 16"), в `tl` и `br` передаются координаты окна. Сортировка объектов будет зависеть от параметра `sort`, как описано выше.

**Примечание:** поля `short_text_from` и `short_text_to` на данный момент возвращают именительный падеж.

### Пример1

    {
        "id": "1234567890abcdefghijkl0987654321",
        "what": "пресненская набережная 12",
        "ll": [
            37.512219,
            55.891277
        ]
    }

-

    {
        "defaultview": "addresses",
        "objects": [
            {
                "city": "Москва",
                "country": "Россия",
                "exact": true,
                "full_text": "Россия, Москва, Пресненская набережная, 12",
                "house": "12",
                "object_type": "другое",
                "point": [
                    37.536831999999997,
                    55.749586999999998
                ],
                "short_text": "Пресненская набережная, 12",
                "short_text_from": "Пресненская набережная, 12",
                "short_text_to": "Пресненская набережная, 12",
                "street": "Пресненская набережная",
                "type": "address",
                "description": "Москва, Россия"
            },
            {
                "city": "Москва",
                "country": "Россия",
                "exact": false,
                "full_text": "Россия, Москва, Пресненская набережная",
                "house": "",
                "object_type": "другое",
                "point": [
                    37.541556999999997,
                    55.746943000000002
                ],
                "short_text": "Пресненская набережная",
                "short_text_from": "Пресненская набережная",
                "short_text_to": "Пресненская набережная",
                "street": "Пресненская набережная",
                "type": "address",
                "description": "Москва, Россия"
            }
        ]
    }


### Пример 2

    {
        'what': u'Краснопресненская набережная 12',
        'll': [37.553330000000003, 55.754047]
    }

-

    {
        "objects": [{
            "city": "Москва",
            "description": "Москва, Россия",
            "full_text": "Россия, Москва, Краснопресненская набережная, 12",
            "point": [37.556387999999998, 55.754202999999997],
            "house": "12",
            "object_type": "другое",
            "exact": true,
            "street": "Краснопресненская набережная",
            "country": "Россия",
            "short_text": "Краснопресненская набережная, 12",
            "short_text_from": "Краснопресненская набережная, 12",
            "short_text_to": "Краснопресненская набережная, 12",
            "type": "address"
        }],
        "defaultview": "addresses"
    }

### Допустимые параметры запроса

*  Вариант 1
    *   ⋮ __what__ `t: point`     точка на карте
        *   ⋮ __response__ `t: point`     объект ответа целиком
    *    __id__ `t: uuid4`     идентификатор сессии пользователя
        *   ⋮ __response__ `t: uuid4`     объект ответа целиком
    *    __results__ `t: integer`     ограничение на количество возвращаемых результатов
    *    __skip__ `t: integer`     начиная с какого результата выводить ответ
    *    __sort__ `t: string` `v: dist/uniform`    порядок сортировки: dist (по умолчанию) - по расстоянию от центра; uniform - по релевантности, независимо от расстояния
*  Вариант 2
    *   ⋮ __ll__ `t: point`     центр области поиска
        *   ⋮ __response__ `t: point`     объект ответа целиком
    *   ⋮ __what__ `t: string`    `min-length: 1` название организации или адрес
    *    __id__ `t: uuid4`     идентификатор сессии пользователя
        *   ⋮ __response__ `t: uuid4`     объект ответа целиком
    *    __results__ `t: integer`     ограничение на количество возвращаемых результатов
    *    __skip__ `t: integer`     начиная с какого результата выводить ответ
    *    __sort__ `t: string` `v: dist/uniform`    порядок сортировки: dist (по умолчанию) - по расстоянию от центра; uniform - по релевантности, независимо от расстояния
*  Вариант 3
    *   ⋮ __br__ `t: point`     нижняя правая точка области поиска
        *   ⋮ __response__ `t: point`     объект ответа целиком
    *   ⋮ __tl__ `t: point`     верхняя левая точка области поиска
        *   ⋮ __response__ `t: point`     объект ответа целиком
    *   ⋮ __what__ `t: string`    `min-length: 1` название организации или адрес
    *    __id__ `t: uuid4`     идентификатор сессии пользователя
        *   ⋮ __response__ `t: uuid4`     объект ответа целиком
    *    __results__ `t: integer`     ограничение на количество возвращаемых результатов
    *    __skip__ `t: integer`     начиная с какого результата выводить ответ
    *    __sort__ `t: string` `v: dist/uniform`    порядок сортировки: dist (по умолчанию) - по расстоянию от центра; uniform - по релевантности, независимо от расстояния

### Допустимые параметры ответа

*   ⋮ __defaultview__ `t: string` `v: addresses/organizations`    вкладка, которую приложение должно по умолчанию показать пользователю
*   ⋮ __objects__ `t: array`     список всех найденных адресов и/или организаций
    *   ⋮ __city__ `t: string`     город
    *   ⋮ __country__ `t: string`     страна
    *   ⋮ __exact__ `t: boolean`     точно ли определен адрес
    *   ⋮ __full_text__ `t: string`     полный адрес
    *   ⋮ __house__ `t: string`     дом
    *   ⋮ __object_type__ `t: string` `v: аэропорт/организация/другое`    классификация объекта или организации
    *   ⋮ __point__ `t: point`     координаты объекта или организации
        *   ⋮ __response__ `t: point`     объект ответа целиком
    *   ⋮ __short_text__ `t: string`     короткий адрес
    *   ⋮ __street__ `t: string`     улица
    *   ⋮ __type__ `t: string` `v: address/organization`    тип объекта - адрес или организация
    *    __description__ `t: string`     мелко-подробности
    *    __oid__ `t: string`     идентификатор объекта
    *    __short_text_from__ `t: string`     короткий адрес после предлога ОТ (откуда)
    *    __short_text_to__ `t: string`     короткий адрес после предлога ДО (куда)

<a name="request_get_user_messages"></a>
## get_user_messages
### Описание

Запрос сообщений из чата пользователя.

В запрос приходит идентификатор авторизованного пользователя и возвращаются сообщения
из открытого чата пользователя и службы поддержки. Запрос доступен только для авторизованных пользователей.
Если открыт чатов нет, то возвращается пустой список сообщений и признаки того, что чат закрыт и скрыт.

### Пример

    {
        "id": "1234567890abcdefghijkl0987654321", # Идентификатор пользователя
    }

-

    {
        "chat_open": true, # Признак открыт или закрыт чат
        "chat_visible": false, # Признак видим или нет чат
        "support_name": "test", # Имя сотрудника службы поддержки
        "avatar_url": "1", # Код аватара
        "messages": [
        {
            "author": "user|support" # Автор сообщения
            "body": "Текст сообщения"
            "type": "text"
            "timestamp": "2013-03-13T09:30:00+0000"
        }
        ]
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __chat_open__ `t: boolean`     Открыт ли чат
*   ⋮ __chat_visible__ `t: boolean`     Видим ли чат
*   ⋮ __messages__ `t: array`     Переписка с службой поддержки
    *   ⋮ __author__ `t: string`     автор
    *   ⋮ __body__ `t: string`     сообщение
    *   ⋮ __timestamp__ `t: string`  `f: date-time`   время сообщения
    *   ⋮ __type__ `t: string`     Тип сообщения
*   ⋮ __new_messages__ `t: integer`     Количество новых сообщений
*    __avatar_url__ `t: string`     Ссылка на аватар сотрудника поддержки
*    __support_name__ `t: string`     Имя сотрудника поддержки

<a name="request_get_user_settings"></a>
## get_user_settings
https://st.yandex-team.ru/TAXIBACKEND-5620

У каждой настройки свой таимстемп. Клиент синхронизирует время с сервером и отвечает за генерацию таимстемпов. В ответе ручки launch передаётся хеш от всех настроек. Таким образом клиент понимает нужно ли обновлять настройки с сервера.

Если настройки сохранить не удалось клиент сохраняет настройки локально с таймстемпом. При загрузке настроек с сервера клиент сверяет таймстемпы локальных настроек с тем что он получил с бекенда.

На клиенте есть дефолтные значения всех настроек на случай если загрузить настройки с сервера не удаётся.

`id` - id пользователя

**Получение настроек**:

    /3.0/get-user-settings
    {
        "id": "00060bd51ffc4498aa8afbdcbb0d5ead"
    }

Ответ:

Если пользователь авторизован и настройки сохранены

    200
    {
        "settings": {
            "tips": {
                "value": 5,
                "timestamp": "2015-12-01T17:08:18+0300"
            }
        },
            "user_settings_hash": "abcdefg"
    }

Настройки, которые пользователь не сохранял, но есть дефолтные значения на бекенде, будут без таимстемпа

    200
    {
        "settings": {
            "tips": {
                "value": 0,
            }
        },
            "user_settings_hash": "abcdefg"
    }

Если пользователя не удалось найти

    404
    {}

Если пользователь неавторизован

    401
    {}

**launch**

Новое поле %%user_settings_hash%%

    {
        ...
        "user_settings_hash": "abcdefg"
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа

*    __settings__ `t: object`     значения и таимстемпы настроек
*    __user_settings_hash__ `t: string`     хеш от настроек

<a name="request_getreferral"></a>
## getreferral
### Описание

Ручка возвращает реферальные промокоды, сгенерированные данным пользователем.
В настоящий момент у пользователя может быть только один промокод.
Если в момент обращения к ручке у пользователя не было промокода,
он будет сгенерирован автоматически.

Генерация промокода может быть доступна не всем пользователям или не во всех
геозонах. В этом случае бекенд возвращает код 406. Если во время генерации
промокода возникла гонка, возвращается код 409.

Обязательные параметры:
* `id` - id пользователя

Ручка требует авторизации и токена, как `couponcheck`.

В случае успеха возвращает массив объектов с информацией о промокодах.
В настоящий момент в массиве всегда будет один элемент. Чтобы сделать поведение клиента
предсказуемым, в случае, если элементов больше одного, следует брать последний.

Каждый объект имеет следующие поля:
* `promocode` - "секретный" код промокода,
* `value` - номинал промокода,
* `currency` - код валюты промокода,
* `rides_count` - общее число поездок по промокоду,
* `rides_left` - оставшееся число поездок,
* `descr` - описание промокода для экрана приложения (в локали пользователя), 
* `message` - текст-ссылка на промокод для отправки в социальные сети и т.п.

Примечание: текст в `descr` может зависеть от числа оставшихся поездок и других параметров
промокода.

### Пример 1

    {
        "id": "1234567890abcdefghijkl0987654321",
    }

-

    [
        {
            "promocode": "z0wg23h",
            "value": 300,
            "currency": "RUB",
            "rides_count": 5,
            "rides_left": 3,
            "descr": "Подари другу промокод на 300 руб",
            "message": "Я пользуюсь Яндекс.Такси. Получи скидку 300 руб: https://taxi.yandex.ru/referrals/z0wg23h",
        }
    ]

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __format_currency__ `t: boolean`      если передан, то в ответе передаем валюты в определенном формате

### Допустимые параметры ответа

*   ⋮ __response__ `t: promocode_referral`     объект ответа целиком

<a name="request_launch"></a>
## launch
### Описание

Запрос инициализации для приложений.

Предназначен для первого запуска приложения и всех случаев, когда приложению неизвестно текущее
состояние пользователя - какие заказы еще не завершены, какое сейчас точное время, какие сообщения
нужно показать пользователю и так далее. Если пользователь был заблокирован, в ответе launch будет
передана информация о продолжительности блокировки.

В этом запросе происходит выдача или замена идентификатора пользовательской сессии, который нужен
для оформления заказов. Если приложение не передает параметр `id`, то сервер выдает новый
идентификатор. В противном случае сервер старается сохранить существующий идентификатор для
пользователя, но может выдать новый, который следует использовать вместо старого во всех
последующих запросах.

### Стартап

Стартап - это универсальный для всех мобильных приложений Яндекса способ инициализации приложений.
В следующих версиях протокола останется только один из запросов `launch`, `startup`, но на текущий
момент необходимо каждый раз делать оба этих запроса вместе при запуске клиента Такси.

Описание запроса `startup` находится по адресу
http://wiki.yandex-team.ru/YandexMobile/generic-startup.

### Фильтр платежей в paymentstatuses

Значением поля `payment_statuses_filter` является список меток (строк):

* `"debt"` - есть неоплаченные заказы
* `"need_cvn"` - один из платежей требует ввода CVN
* `"need_accept"` - один из платежей требует подтвереждения стоимости
  поездки
* `"can_be_paid_by_card"` - один из последних платежей может быть
  оплачен картой

**Рекомендация**: содержимое списка (если он не пустой) передавать в
paymentstatuses в неизменном виде.

### Идентификатор устройства

По причинам, описанным в TAXIBACKEND-2742, приложения должны передавать
на бекенд идентификатор устройства. Идентификатор передается в поле `device_id`
в виде строки символов. Бекенд не пытается интерпретировать структуру
идентификатора и обращается с ним как с непрозрачной константой.


### Текущие изменения
У элементов в массиве "orders" сервер вернет список текущих активных изменений
по данному заказу (в поле `"pending_changes"`).

### Реферальные промокоды
Если данному пользователю можно генерировать реферальные промокоды, в ответе ручки
будет флаг `can_generate_referrals`. Если флаг отсутствует или равен `false`,
соответствующий пункт меню должен быть скрыт.


### Информация об обновлении приложения

Информация носит *рекомендательный* характер!

В ответе `/3.0/launch` может прийти объект `"version_info"`. Если данный
объект отсутствует, не надо предлагать обновляться. Содержимое объекта:

* `"current_version": "X.Y.Z.P"` - последняя доступная версия приложения
  (например, "3.16.3.7397" для Android и "3.54.4558" для iOs)
* `"update_notification_interval": 100500` - *минимальный* интервал в
  секундах между предложениями обновиться

Сравнивать версии необходимо, приведя все числа из строки с версией к
целым числам, отсутствующие числа считать нулями:

    версия на   current_version     рекомендоваать обновиться
    клиенте

    3.4              3.4                нет
    3.4.5            3.4                нет
    3.5              3.4                нет
    3.4              3.4.5              да
    3.4              3.5                да

Если нужно предлагать обновляться, то после показа соответствующего
предложения необходимо запомнить время последнего показа. В следующий
раз предлагать не ранее, чем через `"update_notification_interval"`
секунд.

Формат сообщения об обновлении не оговорён (определяется самим
приложением).


### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "device_id": "09876554321zxcvbnm"
    }

-

    {
        "authorized": false,
        "info": [],
        "loyal": false,
        "orders": [],
        "server_time": "2013-03-13T08:57:22+0000",
        "uuid": "1234567890mnopqrstuvwx",
        "blocked": {
            "blocked": "2013-03-13T09:30:00+0000",
            "type": "phone"
        },
        "payment_statuses_filter": []
    }


-

    {
        "id": "1234567890abcdefghijkl0987654321",
        "device_id": "09876554321zxcvbnm"
    }

-

    {
        "authorized": false,
        "info": [],
        "loyal": false,
        "orders": [
            {
                "orderid": "1234567890mnopqrstuvwx",
                "due": "2013-03-13T09:30:00+0000",
                "status": "transporting",
                "pending_changes": [
                    {
                        "change_id": "7116f3e79bc843a09ef13756b04d19dc",
                        "name": "comment",
                        "value": "some comment",
                        "status": "pending"
                    }
                ]
            }
        ],
        "server_time": "2013-03-13T08:57:22+0000",
        "uuid": "1234567890mnopqrstuvwx",
        "blocked": {
            "blocked": "2013-03-13T09:30:00+0000",
            "type": "phone"
        },
        "payment_statuses_filter": [],
        "version_info":{
            "current_version": "3.50.4366",
            "update_notification_interval": 604800
        },
    }

### Допустимые параметры запроса

*    __apns_token__ `t: string`    `min-length: 1` токен push-сообщений Apple
*    __apns_type__ `t: string` `v: release-distr/inhouse-distr/inhouse-dev`    вид сборки приложения
*    __c2dm_token__ `t: string`    `min-length: 1` токен push-сообщений Google (deprecated)
*    __device_id__ `t: string`    `min-length: 1` идентификатор устройства (idfa или android_id)
*    __gcm_token__ `t: string`    `min-length: 1` токен новых push-сообщений Google
*    __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __mpns_url__ `t: string`   `r: ^https?://[a-z0-9]+\.notify\.live\.net/`  URL для push-сообщений Microsoft
*    __wns_url__ `t: string`     URL для push-сообщений Windows Phone 10

### Допустимые параметры ответа

*   ⋮ __authorized__ `t: boolean`     пользователь авторизован
*   ⋮ __loyal__ `t: boolean`     лояльный пользователь
*   ⋮ __server_time__ `t: string`  `f: date-time`   точное UTC-время
*   ⋮ __uuid__ `t: string`     идентификатор для стартапа
*    __ask_feedback__ `t: object`     заказ, по которому нужно предложить оставить отзыв
    *   ⋮ __due__ `t: string`  `f: date-time`   время подачи машины
    *   ⋮ __orderid__ `t: uuid4`     идентификатор заказа
        *   ⋮ __response__ `t: uuid4`     объект ответа целиком
    *   ⋮ __parkid__ `t: string`    `min-length: 6` идентификатор таксопарка
*    __blocked__ `t: object`     информация о блокировке пользователя
    *   ⋮ __blocked__ `t: string`  `f: date-time`   время окончания блокировки
    *   ⋮ __type__ `t: string` `v: phone`    тип блокировки
*    __can_generate_referrals__ `t: boolean`     true, если пользователю доступна генерация промокодов
*    __chat__ `t: object`     Информация о чате пользователя
    *   ⋮ __new_chat_messages__ `t: integer`     время подачи машины
    *   ⋮ __support_timestamp__ `t: string`  `f: date-time`   UTC время последнего ответа службы поддержки
*    __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __info__ `t: array`     информационные сообщения
    *   ⋮ __header__ `t: string`     заголовок
    *   ⋮ __message__ `t: string`     текст
    *   ⋮ __time__ `t: string`  `f: date-time`   время, раньше которого нельзя показывать сообщение
*    __name__ `t: string`    `min-length: 1` имя авторизованного пользователя
*    __orders__ `t: array`     незавершенные заказы пользователя
    *   ⋮ __due__ `t: string`  `f: date-time`   время подачи машины
    *   ⋮ __orderid__ `t: uuid4`     идентификатор заказа
        *   ⋮ __response__ `t: uuid4`     объект ответа целиком
    *   ⋮ __pending_changes__ `t: array`     еще не примененные изменения по заказу
    *   ⋮ __status__ `t: order_status`     статус заказа
        *   ⋮ __response__ `t: order_status`     объект ответа целиком
    *    __service_level__ `t: service_level`     положения селектора дёшево-комфортно
        *   ⋮ __response__ `t: service_level`     объект ответа целиком
*    __payment_statuses_filter__ `t: payment_statuses_filter`     типы платеже, принимаемые в параметре filter ручки paymentstatuses
    *   ⋮ __response__ `t: payment_statuses_filter`     объект ответа целиком
*    __phone__ `t: phone`     авторизованный номер телефона пользователя
    *   ⋮ __response__ `t: phone`     объект ответа целиком
*    __phones__ `t: object`     авторизованные и неавторизованные номера телефонов пользователя в Паспорте
    *    __\+\d+__ `t: boolean`     номер авторизован
*    __show_me_min_distance__ `t: integer`     Минимальное количество метров до пина, при котором отображается буква Я
*    __token_valid__ `t: boolean`     true, если oauth-токен валиден
*    __use_new_smooth_movement__ `t: boolean`     true, чтобы клиент включил новое плавное движение
*    __yandex_staff__ `t: boolean`     пользователь является сотрудником Яндекса

<a name="request_lbs"></a>
## lbs
### Описание

Доступ к сервису LBS.

Подробнее: http://wiki.yandex-team.ru/YandexMobile/lbs/api/json

Сервер Такси подписывает запрос своим `api_key` автоматически.

### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "common": {
            "version": "1.0"
        },
        "gsm_cells": [
            {
                "cellid": "1234",
                "countrycode": "351",
                "lac": "54321",
                "operatorid": "2"
            }
        ],
        "ip": {
            "address_v4": "192.168.0.1"
        },
        "wifi_networks": [
            {
                "mac": "12:e2:d4:c8:76:9b"
            }
        ]
    }

-

    {
        "position": {
            "altitude": 0.0,
            "altitude_precision": 30.0,
            "latitude": 56.123470100000003,
            "longitude": 34.5213409400000003,
            "precision": 100000,
            "type": "ip"
        }
    }

### Допустимые параметры запроса


### Допустимые параметры ответа


<a name="request_nearestparks"></a>
## nearestparks
### Описание

Список таксопарков рядом с заданной точкой.

Ручка используется для поиска телефонов такси в тех населённых пунктах, где ещё не действует служба Я.Такси.


### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "ll": [61.471157,57.014094],
        "results": 4
    }

-

    {
        "objects": [{
            "phone": "+7 (495) 222-25-42",
            "name": "Посейдон"
        }, {
            "phone": "+7 (495) 518-78-80",
            "name": "Такси-мытищи.РФ"
        }, {
            "phone": "+7 (495) 999-99-99",
            "name": "Такси Пилот"
        }, {
            "phone": "+7 (495) 665-16-65",
            "name": "Старое Такси Москва"
        }]
}

### Допустимые параметры запроса

*   ⋮ __ll__ `t: point`     центр области поиска
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __results__ `t: integer`     ограничение на количество возвращаемых результатов
*    __skip__ `t: integer`     начиная с какого результата выводить ответ

### Допустимые параметры ответа

*   ⋮ __objects__ `t: array`     список контактной информации
    *   ⋮ __name__ `t: string`     название таксопарка
    *   ⋮ __phone__ `t: string`     номер телефона таксопарка

<a name="request_nearestposition"></a>
## nearestposition
### Описание

Ручка предназначена для наилучшего угадывания, где сейчас находится пользователь.
На вход получает id пользователя, координаты устройства и погрешность определения координат в метрах.
Возвращает первую найденную точку из списка:

1. точный результат обратного геокодирования, если погрешность dx меньше 20 метров
1. адреса из истории пользователя (если несколько, то ближайший к точке)
1. точный результат обратного геокодирования
1. точные популярные адреса (если несколько, то ближайший к точке)
1. результат притягивания к домам
1. неточный результат геокодирования

лежащую в указанных пределах гео-позиционирования. Формат вывода совпадает с форматом geosearch.
Если прислан радиус неточности менее 100 метров, он будет увеличен до 100 метров.

Если значением параметра `not_sticky` будет истина, то будет возвращён результат обратного геокодирования
по координатам, переданными на вход. Если это не точный адрес, и до ближайшей дороги окажется больше 100
метров, то будет возвращён результат обратного геокодирования ближайшей точки на дороге с её координатами.

Если в ответе вернётся "comment" или "porchnumber", они должны быть переданы в заказ.

**Примечание:** поля `short_text_from` и `short_text_to` на данный момент возвращают именительный падеж.


### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "ll": [37.5368, 55.7495],
        "dx": 10
    }

-

    {
        "city": "Москва",
        "country": "Россия",
        "exact": true,
        "full_text": "Россия, Москва, Пресненская набережная, 12",
        "house": "12",
        "object_type": "другое",
        "point": [
            37.536831999999997,
            55.749586999999998
        ],
        "short_text": "Пресненская набережная, 12",
        "short_text_from": "Пресненская набережная, 12",
        "short_text_to": "Пресненская набережная, 12",
        "street": "Пресненская набережная",
        "type": "address",
        "description": "Москва, Россия",
        "comment": "остановитесь у дома",
        "porchnumber": "2"
    }

### Допустимые параметры запроса

*   ⋮ __dx__ `t: integer`     погрешность местоположения в метрах
*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __ll__ `t: point`     центр области поиска
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __not_sticky__ `t: boolean`     не притягивать (вернуть адрес точки из Карт без притягивания)

### Допустимые параметры ответа

*   ⋮ __city__ `t: string`     город
*   ⋮ __country__ `t: string`     страна
*   ⋮ __exact__ `t: boolean`     точно ли определен адрес
*   ⋮ __full_text__ `t: string`     полный адрес
*   ⋮ __house__ `t: string`     дом
*   ⋮ __object_type__ `t: string` `v: аэропорт/организация/другое`    классификация объекта или организации
*   ⋮ __point__ `t: point`     координаты объекта или организации
    *   ⋮ __response__ `t: point`     объект ответа целиком
*   ⋮ __short_text__ `t: string`     короткий адрес
*   ⋮ __street__ `t: string`     улица
*   ⋮ __type__ `t: string` `v: address/organization`    тип объекта - адрес или организация
*    __comment__ `t: string`     комментарий к заказу
*    __description__ `t: string`     мелко-подробности
*    __oid__ `t: string`     идентификатор объекта
*    __porchnumber__ `t: string`     подъезд
*    __short_text_from__ `t: string`     короткий адрес после предлога ОТ (откуда)
*    __short_text_to__ `t: string`     короткий адрес после предлога ДО (куда)

<a name="request_nearestzone"></a>
## nearestzone
### Описание

Поиск ближайшей геозоны с тарифами.

В запросе нужно указать точку для которой нужно найти ближайшую геозону
с привязанными тарифами. Радиус поиска ограничен 30км. 

В ответ ручка возвращает название геозоны.

### Пример

    {
        "point": [61.043575, 56.903985]
    }

-

    {
        "nearest_zone": "ekb"
    }

### Допустимые параметры запроса

*   ⋮ __point__ `t: point`     точка
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа

*    __nearest_zone__ `t: string`     ближайшая зона с тарифами

<a name="request_order"></a>
## order
### Описание

Заказ такси.

В зависимости от времени подачи (параметр `due`), сервер распределяет заказ в один из двух режимов -
срочные и на точное время. Заказ становится срочным, если его время подачи не далее 25 минут
(изменение этой границы считается обратно-совместимым в рамках протокола), в противном случае он
считается сделанным на точное время.

Если время подачи не передано (параметр `due` отсутствует), заказ считается оформленным
"на ближайшее время". В этом случае заказ обрабатывается в режиме срочного, а время подачи
устанавливается сервером в зависимости от текущей ситуации.

Для срочного заказа `status` будет иметь значение `search` - это означает, что сервер ищет машины
среди ближайших к пользователю, учитывая требования. Пользователю нужно показать экран поиска такси
с радаром и дальше руководствоваться указаниями запроса `taxisearch`.

Для заказа на точное время `status` будет иметь значение `scheduling` - это означает, что сервер
предлагает заказ разным компаниям с учетом требований, но вне зависимости от текущего
местоположения машин. Пользователю нужно показать экран распределения заказа с песочными часами и
дальше руководствоваться указаниями запроса `taxiontheway`.

Клиент должен указать пожелания по соотношению цена/качество одним из двух взаимоисключающих
способов: определив список допустимых классов в поле `class` ИЛИ определив значение `service_level`
от 0 (самая дешёвая поездка) до 100 (самая комфортная поездка).

**Важно!** Поля `service_level` и `class` не могут быть переданы одновременно!

Для частичной или полной оплаты заказа купоном необходимо передать секретный код купона в
параметре `requirements.coupon`. Приложение должно проверять правильность ввода секретного кода
купона перед отправкой с помощью [алгоритма Луна](http://en.wikipedia.org/wiki/Luhn_algorithm)
(контрольный разряд - последний). Если секретный код введен правильно и купон еще действителен
(существует, не потрачен ранее, не удален и т.д.), сервер возвращает в ответе параметр `coupon`,
содержащий флаг валидности купона и номинал купона в валюте текущего города. Если секретный код не
валиден, сервер возвращает флаг со значением `false` и не возвращает номинал; либо, если в запросе
присутствовал параметр `force_coupon: true`, запрос завершается с кодом ошибки 406 Not acceptable.
В последнем случае в теле ответа также будет содержаться флаг, свидетельствующий о невалидности купона.



Для заказов с терминалов или из колл-центра (если передано поле `terminal` или `callcenter`) номер телефона
не нужно авторизовывать. Номер будет привязан к идентификатору,
полученному из launch (для каждого нового заказа с терминала необходимо
получать новый идентификатор в launch). После создания заказа на
указанный номер телефона придёт СМС с информацией о том, что заказ
принят. Вместе с тем запрос на создание заказа может быть отклонён по
следующим причинам:

Если в текущей зоне установлен принудительный сурж, и пользователь подтвердил
его принятие, необходимо передать параметр `forced_surge` с ключём `value`, в
котором будет содержаться значение суржа, на которое согласился пользователь.

Если среди переданных классов есть `pool` или `service_level` сводящийся к нему,
необходимо так же чтобы было передано число мест.

  * 400 - тело запроса не является валидным JSON-объектом
  * 400 - отсутствует один или несколько обязательных параметров
  * 400 - некорректный номер телефона
  * 400 - не найдена зона
  * 400 - не передано поле `payment.cardid` при оплате картой
  * 401 - необходимо получить новый идентификатор в launch
  * 403 - запрещено делать заказ для переданного номера телефона или для
    конкретного терминала; подробности в теле:
    `{"blocked": "2015-...", "type": type}`, где type может принимать
    значения `"id"` (заблокировано для терминала) или `"phone"`
    (блокировка переданного номера телефона)
  * 406 - передан некорректный промокод, в теле ответа:
    `{"error": {"code": "WRONG_COUPON", "text": text}, "coupon": {"valid": false, "valid_any": true/false}}`
    `valid_any` указывает, может ли промокод быть действующим при других условиях (другой способ оплаты, другой город и т.п.)
  * 406 - есть долг по предыдущим заказам (с этого телефона, устройства, или по этой карте), в теле ответа:
    `{"error": {"code": "DEBT_USER", "text": text}}`
  * 406 - передана карта, не привязанная к данному пользователю, в теле ответа:
    `{"error": {"code": "UNKNOWN_CARD", "text": text}}`
  * 406 - передана карта, отмеченная как недействующая, в теле ответа:
    `{"error": {"code": "UNUSABLE_CARD", "text": text}}`
  * 406 - есть заказ в обработке для данного номера, в теле ответа:
    `{"error": {"code": "TOO_MANY_UNFINISHED_ORDERS", "text": text}}`
  * 406 - при попытке вызвать корпоративное такси, когда пользователь не является корпоративным клиентом:
    `{"error": {"code": "NOT_CORP_CLIENT", "text": text}}`
  * 406 - при попытке вызвать корпоративное такси, когда пользователь превысил лимит:
    `{"error": {"code": "CORP_LIMIT_EXCEEDED", "text": text}}`
  * 406 - когда нельзя вызвать корпоративное такси в выбранном городе:
    `{"error": {"code": "CORP_CITY_DISABLED", "text": text}}`
  * 406 - когда нельзя вызвать корпоративное такси по данной категории:
    `{"error": {"code": "CORP_CLASS_DISABLED", "text": text}}`
  * 406 - переданы неподдерживаемые требования, в теле ответа:
    `{"error": {"code": "WRONG_REQUIREMENTS", "text": text, "wrong_requirements": ["creditcard", "nosmoking"]}}`
    либо несовместимые данные в требованиях (`requirements`) и способе оплаты (`payment.type`) 
    `{"error": {"code": "WRONG_REQUIREMENTS", "text": text}}`
  * 406 - переданный тариф не может быть применен (например, неактивен в указанное время подачи):
    `{"error": {"code": "TARIFF_IS_UNAVAILABLE", "text": text}}`
  * 406 - переданный тариф не может быть применен (например, не применяется для отложенных заказов):
    `{"error": {"code": "TARIFF_IS_RESTRICTED", "text": text}}`
  * 406 - переданный тип оплаты не может быть применен (например, не действует на данном тарифе):
    `{"error": {"code": "PAYMENT_TYPE_UNACCEPTABLE", "text": text}}`
  * 406 - некорректные аутентификационные данные (например, невалидные или поддельные куки):
    `{"error": {"code": "MISSING_UID", "text": text}}`
  * 406 - значение сурж-коэффициента на данный момент отличается от переданного в запросе (на клиенте нужно получить новый):
    `{"error": {"code": "FORCED_SURGE_CHANGED", "text": text}}`
  * 406 - цена на данный момент отличается от присланной ранее в `routestats` (на клиенте нужно ещё раз пойти в `routestats`):
    `{"error": {"code": "PRICE_CHANGED", "text": text}}`
  * 429 - есть незавершённые заказы, и их число больше разрешенного
  

**Особенности проверки купонов в тестинге:**
  По умолчанию в тестинге отключена проверка, что парк имеет право брать купонные заказы
  (т.к. если купонных заказов много, то есть риск, что у парка всегда будет недостаточно комиссий).
  Таким образом, на купонный заказ в тестинге парки никогда не будут исключаться.
  Если требуется, чтобы парки действительно проверялись на право брать купонные заказы,
  то нужно в комментарий заказа добавить следующую строку:

  * `coupon - 1` - парки будут проверяться, как в продакшене (с тестовым балансом, разумеется).

**Для оплаты картой** нужно передавать поле `payment`, содержащее тип и номер карты (см. схему запроса).
Размер чаевых передаётся в поле `tips`. На данный момент поддерживается указание чаевых только в
процентах от суммы заказа.

**Важно!** Нельзя делать заказы чаще, чем раз в 20 секунд. Если делать чаще, сервер будет отвечать
429 Too Many Requests.

**Проверка оплаты картой в тестинге:** в тестинге в комментарий заказа
можно передать специальные значения (`type - value, type - value`),
которые будут иметь следующую интерпретацию:

  * `failcard - 2` - произойдёт переход на оплату наличными, при попытке
    оплаты заказа картой потребуется ввод CVN
  * `payment - yes` - эмулирует успешную процедуру списания средств по
    окончанию поезки (в действительности запрос в биллинг не уйдёт)
  * `payment - payable` - по окончанию поездки будет отправлен реальный
    запрос в тестовый биллинг; в зависимости от ответа биллинга клиенту
    либо будет заблокирован, либо блокировка будет снята
  * `needcvn - 5` - карта будет требовать ввода CVN

Подробнее: https://wiki.yandex-team.ru/taxi/backend/card-in-testing


Можно передать поле `"dont_call": true` или `"dont_call": false` - это позволит
передать (или не передать) водителю сообщение с просьбой не звонить.

Можно передать поле `"dont_sms": true` или `"dont_sms": false` - это позволит
не смсить пользователю

Количество пассажиров передаётся через requirements: 

    {
        "requirements": {"capacity": 2}
    }


### Пример заказа машин эконом-класса

    {
        "id": "1234567890abcdefghijkl0987654321",
        "city": "Москва",
        "class": [
            "econom"
        ],
        "parks": [
            "000111",
            "000112"
        ],
        "requirements": {
            "animaltransport": true,
            "coupon": "014444444443"
        },
        "payment": {
            "type": "cash"
        },
        "route": [
            {
                "country": "Россия",
                "fullname": "Россия, Москва, Новосущевская, 1",
                "geopoint": [
                    33.6,
                    55.1
                ],
                "locality": "Москва",
                "porchnumber": "1",
                "premisenumber": "1",
                "thoroughfare": "Новосущевская"
            },
            {
                "country": "Россия",
                "fullname": "Россия, Москва, 8 Марта, 4",
                "geopoint": [
                    33.1,
                    52.1
                ],
                "locality": "Москва",
                "porchnumber": "",
                "premisenumber": "4",
                "thoroughfare": "8 Марта"
            }
        ],
        "forced_surge": {
            "value": 2.5
        },
        "due": "2013-04-01T14:00:00+0400",
        "dont_call": true,
        "dont_sms": true
    }

-

    {
        "orderid": "1234567890mnopqrstuvwx0987654321",
        "status": "search",
        "coupon": {
            "valid": true,
            "value": 300
        }
    }

### Пример заказа самых дешёвых машин

    {
        "id": "1234567890abcdefghijkl0987654321",
        "city": "Москва",
        "service_level": 0,
        "parks": [],
        "requirements": {
            "nosmoking": true
        },
        "payment": {
            "type": "cash"
        },
        "route": [
            {
                "country": "Россия",
                "fullname": "Россия, Москва, Новосущевская, 1",
                "geopoint": [
                    33.6,
                    55.1
                ],
                "locality": "Москва",
                "porchnumber": "1",
                "premisenumber": "1",
                "thoroughfare": "Новосущевская"
            },
            {
                "country": "Россия",
                "fullname": "Россия, Москва, 8 Марта, 4",
                "geopoint": [
                    33.1,
                    52.1
                ],
                "locality": "Москва",
                "porchnumber": "",
                "premisenumber": "4",
                "thoroughfare": "8 Марта"
            }
        ],
        "due": "2013-04-01T14:00:00+0400"
    }

-

    {
        "orderid": "1234567890mnopqrstuvwx0987654321",
        "status": "search"
    }

### Пример неудачного запроса с обязательным использованием невалидного купона

    {
        "id": "1234567890abcdefghijkl0987654321",
        "city": "Москва",
        "class": [
            "econom"
        ],
        "parks": [],
        "requirements": {
            "coupon": "014444444443"
        },
        "payment": {
            "type": "cash"
        },
        "route": [
            {
                "country": "Россия",
                "fullname": "Россия, Москва, Новосущевская, 1",
                "geopoint": [
                    33.6,
                    55.1
                ],
                "locality": "Москва",
                "porchnumber": "1",
                "premisenumber": "1",
                "thoroughfare": "Новосущевская"
            },
            {
                "country": "Россия",
                "fullname": "Россия, Москва, 8 Марта, 4",
                "geopoint": [
                    33.1,
                    52.1
                ],
                "locality": "Москва",
                "porchnumber": "",
                "premisenumber": "4",
                "thoroughfare": "8 Марта"
            }
        ],
        "due": "2013-04-01T14:00:00+0400",
        "force_coupon": true
    }

-

    HTTP/1.1 406 Not Acceptable
    ...HTTP-заголовки...

    {
        "orderid": "1234567890mnopqrstuvwx0987654321",
        "status": "failed",
        "coupon": {
            "valid": false
        }
    }

### Пример заказа с оплатой картой

    {
        "id": "1234567890abcdefghijkl0987654321",
        "city": "Москва",
        "service_level": 50,
        "parks": [],
        "route": [
            {
                "country": "Россия",
                "fullname": "Россия, Москва, Новосущевская, 1",
                "geopoint": [
                    33.6,
                    55.1
                ],
                "locality": "Москва",
                "porchnumber": "1",
                "premisenumber": "1",
                "thoroughfare": "Новосущевская"
            },
            {
                "country": "Россия",
                "fullname": "Россия, Москва, 8 Марта, 4",
                "geopoint": [
                    33.1,
                    52.1
                ],
                "locality": "Москва",
                "porchnumber": "",
                "premisenumber": "4",
                "thoroughfare": "8 Марта"
            }
        ],
        "due": "2015-03-31T14:00:00+0400",
        "payment": {
            "type": "card"
            "payment_method_id": "card-12345678",
        },
        "tips": {
            "type": "percent",
            "value": 5
        }
    }

-

    {
        "orderid": "1234567890mnopqrstuvwx0987654321",
        "status": "search"
    }

### 3.0

При переходе клиентов на версию 3.0 необходимо унифицировать форматы
адресов, приходящих в запрос /3.0/order, с форматом ответов
/3.0/geosearch (а также /3.0/nearestposition и т.д.). Для этого запрос
geosearch расширяется новыми полями:

* `fullname`
* `short_text`
* `short_text_from`
* `short_text_to`
* `country`
* `locality`
* `thoroughfare`
* `premisenumber`
* `type`
* `object_type`
* `geopoint`
* `exact`

Для заказа на конкретную точку (а не на адрес, см. TAXIBACKEND-2610)
в первом элементе массива `route` следует добавить атрибут
`use_geopoint`: `true` (см. пример). Поле необязательное; по умолчанию
считается, что заказ осуществлен на адрес. 

Пример:

    {
        "id": "1234567890abcdefghijkl0987654321",
        "city": "Москва",
        "service_level": 0,
        "parks": [],
        "requirements": {
            "nosmoking": true
        },
        "payment": {
            "type": "cash"
        },
        "route": [
            {
                "country": "Россия",
                "fullname": "Россия, Москва, Новосущевская, 1",
                "short_text": "Новосущевская, 1",
                "short_text_from": "Новосущевская, 1",
                "short_text_to": "Новосущевская, 1",
                "geopoint": [
                    33.6,
                    55.1
                ],
                "locality": "Москва",
                "porchnumber": "1",
                "premisenumber": "1",
                "thoroughfare": "Новосущевская",
                "type": "address",
                "object_type": "другое",
                "exact": true,
                "use_geopoint": true
            },
            {
                "country": "Россия",
                "fullname": "Россия, Москва, 8 Марта, 4",
                "short_text": "8 Марта, 4",
                "short_text_from": "8 Марта, 4",
                "short_text_to": "8 Марта, 4",
                "geopoint": [
                    33.1,
                    52.1
                ],
                "locality": "Москва",
                "porchnumber": "",
                "premisenumber": "4",
                "thoroughfare": "8 Марта",
                "type": "address",
                "object_type": "другое",
                "exact": true
            }
        ],
        "due": "2013-04-01T14:00:00+0400"
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __parks__ `t: excluded_parks`     исключённые таксопарки
    *   ⋮ __response__ `t: excluded_parks`     объект ответа целиком
*   ⋮ __route__ `t: route_in_order`     маршрут заказа
    *   ⋮ __response__ `t: route_in_order`     объект ответа целиком
*    __callcenter__ `t: object`     дополнительные данные, если заказ оформляется из колл-центра
    *    __key__ `t: string`    `min-length: 1` авторизационный ключ
    *    __login__ `t: string`    `min-length: 1` логин оператора
    *    __phone__ `t: phone`     номер телефона, на который оформить заказ
        *   ⋮ __response__ `t: phone`     объект ответа целиком
*    __city__ `t: city`     город
    *   ⋮ __response__ `t: city`     объект ответа целиком
*    __class__ `t: class`     классы автомобилей
    *   ⋮ __response__ `t: class`     объект ответа целиком
*    __clid__ `t: string`    `min-length: 1` идентификатор поставщика предустановленного приложения
*    __client_forwarded_phone__ `t: phone`     контактный номер телефона 
    *   ⋮ __response__ `t: phone`     объект ответа целиком
*    __comment__ `t: string`     комментарий к заказу
*    __corp_cost_center__ `t: string`     Кост-центр корпоративного заказа
*    __dont_call__ `t: boolean`     передать водителю сообщение 'Не звонить'
*    __dont_sms__ `t: boolean`     не смсить пользователю
*    __driverclientchat_enabled__ `t: boolean`     true если клиент поддерживает чат
*    __due__ `t: string`  `f: due_time`   время подачи
*    __force_coupon__ `t: boolean`     не создавать заказ при недействительном купоне
*    __forced_surge__ `t: object`     есть поддержка принудительного суржа
    *   ⋮ __value__ `t: number`     величина суржа, отправленная клиенту
*    __intermediary__ `t: intermediary`     тип посредника
    *   ⋮ __response__ `t: intermediary`     объект ответа целиком
*    __offer__ `t: string`     идентификатор предложения
*    __payment__ `t: payment`     данные для оплаты картой (только при requirements.creditcard=true)
    *   ⋮ __response__ `t: payment`     объект ответа целиком
*    __referral__ `t: string`     идентификатор реферальной ссылки
*    __requirements__ `t: requirements_request`     требования к автомобилю
    *   ⋮ __response__ `t: requirements_request`     объект ответа целиком
*    __selected_promotions__ `t: array`     список выбранных пользователем идентификаторов промо-акций, которые он бы хотел применить к этой поездке
*    __service_level__ `t: service_level`     положение ползунка на шкале дёшево-комфортно
    *   ⋮ __response__ `t: service_level`     объект ответа целиком
*    __started_in_emulator__ `t: boolean`     true если клиент запущен в эмуляторе
*    __terminal__ `t: object`     дополнительные данные, если заказ оформляется с терминала
    *    __id__ `t: string`    `min-length: 1` идентификатор терминала
    *    __key__ `t: string`    `min-length: 1` авторизационный ключ
    *    __phone__ `t: phone`     номер телефона, на который оформить заказ
        *   ⋮ __response__ `t: phone`     объект ответа целиком
*    __tips__ `t: tips`     ?
    *   ⋮ __response__ `t: tips`     объект ответа целиком
*    __zone_name__ `t: string`     название зоны

### Допустимые параметры ответа

*   ⋮ __orderid__ `t: uuid4`     идентификатор созданного заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __status__ `t: order_status`     статус созданного заказа
    *   ⋮ __response__ `t: order_status`     объект ответа целиком
*    __coupon__ `t: coupon_info`     предъявленный к оплате купон
    *   ⋮ __response__ `t: coupon_info`     объект ответа целиком

<a name="request_ordercommit"></a>
## ordercommit
### Описание

Подтверждение заказа. В запрос передаётся идентификатор заказа,
полученный из ответа `/3.0/orderdraft`.

Операция подтверждения идемпотентна. Если сервер ответит ошибкой (или
соединение будет разорвано по таймауту) необходимо повторить запрос с
тем же идентификатором заказа.

Подтверждение заказа приводит к началу обработки заказа: проверяются
кредитная карта, промокод, детектируются спамеры. Поэтому в ответе могут
прийти все те же ошибки, что и в ответе `/3.0/order`.

Если к моменту подтверждения черновик будет удалён (например, с момента
создания черновика прошло слишком много времени), сервер ответит ошибкой
`410`.


### Пример запроса

    {
        "id": "abc123abc123abc123abc123abc123ab",
        "orderid": "1234567890abcdefghijkl0987654321"
    }

### Пример ответа

    {
        "status": "search",
        "coupon": {
            "valid": true,
            "value": 350
        }
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __orderid__ `t: uuid4`     идентификатор ранее созданного заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __status__ `t: order_status`     статус созданного заказа
    *   ⋮ __response__ `t: order_status`     объект ответа целиком
*    __coupon__ `t: coupon_info`     предъявленный к оплате купон
    *   ⋮ __response__ `t: coupon_info`     объект ответа целиком

<a name="request_orderdraft"></a>
## orderdraft
### Описание

Создание черновика заказа. Созданный черновик должен быть подтверждён.

При намерении пользователя оформить заказ необходимо выполнить следующий
порядок действий:

1. создать черновик заказа, получив из `/3.0/orderdraft` идентификатор
   заказа; если сервер ответит ошибкой (либо соединение будет разорвано
   по таймауту), необходимо получить новый идентификатор, создав новый
   черновик;
2. подтвердить созданный заказ, передав в `/3.0/ordercommit` полученный
   на этапе 1 идентификатор заказа; если сервер ответит ошибкой (либо
   соединение будет разорвано по таймауту), неоходимо повторить запрос
   заново с тем же идентификатором заказа.

Создание черновика не приводит к началу обработки заказа, поэтому может
быть создано сколь угодно много черновиков. При создании черновика
сервер не проверяет кооректность введённых параметров, таких как
идентификатор карты, корректность промокода и т.д., - они проверяются на
этапе подтверждения заказа. Но создать черновик можно только с токеном.

Подтверждение заказа является идемпотентной операцией. Соответственно,
заказ может быть подтверждён сколь угодно много раз.

Количество пассажиров передаётся через requirements: 

    {
        "requirements": {"capacity": 2}
    }


### Примеры запросов

Запрос по структуре и содержанию полностью совпадает с `/3.0/order`.


### Пример ответа

    {
        "orderid": "1234567890abcdefghijkl0987654321"
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __parks__ `t: excluded_parks`     исключённые таксопарки
    *   ⋮ __response__ `t: excluded_parks`     объект ответа целиком
*   ⋮ __route__ `t: route_in_order`     маршрут заказа
    *   ⋮ __response__ `t: route_in_order`     объект ответа целиком
*    __callcenter__ `t: object`     дополнительные данные, если заказ оформляется из колл-центра
    *    __key__ `t: string`    `min-length: 1` авторизационный ключ
    *    __login__ `t: string`    `min-length: 1` логин оператора
    *    __phone__ `t: phone`     номер телефона, на который оформить заказ
        *   ⋮ __response__ `t: phone`     объект ответа целиком
*    __city__ `t: city`     город
    *   ⋮ __response__ `t: city`     объект ответа целиком
*    __class__ `t: class`     классы автомобилей
    *   ⋮ __response__ `t: class`     объект ответа целиком
*    __clid__ `t: string`    `min-length: 1` идентификатор поставщика предустановленного приложения
*    __client_forwarded_phone__ `t: phone`     контактный номер телефона 
    *   ⋮ __response__ `t: phone`     объект ответа целиком
*    __comment__ `t: string`     комментарий к заказу
*    __corp_cost_center__ `t: string`     Кост-центр корпоративного заказа
*    __dont_call__ `t: boolean`     передать водителю сообщение 'Не звонить'
*    __dont_sms__ `t: boolean`     не смсить пользователю
*    __driverclientchat_enabled__ `t: boolean`     true если клиент поддерживает чат
*    __due__ `t: string`  `f: due_time`   время подачи
*    __force_coupon__ `t: boolean`     не создавать заказ при недействительном купоне
*    __forced_surge__ `t: object`     есть поддержка принудительного суржа
    *   ⋮ __value__ `t: number`     величина суржа, отправленная клиенту
*    __intermediary__ `t: intermediary`     тип посредника
    *   ⋮ __response__ `t: intermediary`     объект ответа целиком
*    __offer__ `t: string`     идентификатор предложения
*    __payment__ `t: payment`     данные для оплаты картой (только при requirements.creditcard=true)
    *   ⋮ __response__ `t: payment`     объект ответа целиком
*    __referral__ `t: string`     идентификатор реферальной ссылки
*    __requirements__ `t: requirements_request`     требования к автомобилю
    *   ⋮ __response__ `t: requirements_request`     объект ответа целиком
*    __selected_promotions__ `t: array`     список выбранных пользователем идентификаторов промо-акций, которые он бы хотел применить к этой поездке
*    __service_level__ `t: service_level`     положение ползунка на шкале дёшево-комфортно
    *   ⋮ __response__ `t: service_level`     объект ответа целиком
*    __started_in_emulator__ `t: boolean`     true если клиент запущен в эмуляторе
*    __terminal__ `t: object`     дополнительные данные, если заказ оформляется с терминала
    *    __id__ `t: string`    `min-length: 1` идентификатор терминала
    *    __key__ `t: string`    `min-length: 1` авторизационный ключ
    *    __phone__ `t: phone`     номер телефона, на который оформить заказ
        *   ⋮ __response__ `t: phone`     объект ответа целиком
*    __tips__ `t: tips`     ?
    *   ⋮ __response__ `t: tips`     объект ответа целиком
*    __zone_name__ `t: string`     название зоны

### Допустимые параметры ответа

*   ⋮ __orderid__ `t: uuid4`     идентификатор созданного черновика заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

<a name="request_orderhistory"></a>
## orderhistory
### Описание

Получение истории заказов пользователя. В историю попадают заказы со статусом finished или cancelled с ненулевой оплатой.
 
### Пример

    {
      "id": "361df5c5a406412c89eeaba80de517dc"
    }

-

    {  
       "orders": [  
          {  
             "created_time": 1505731537,
             "currency_code": "RUB",
             "destinations": [  

             ],
             "display_surge": false,
             "final_cost": "99.00",
             "item_id": "1505731537:05f79ec6fb4143f2ae22d7c449d6b094",
             "map_image": "https://static-maps.yandex.ru/1.x/?l=map&size=800,400&cr=0&lg=0&pt=37.639689,55.735297,comma_red&key=ADfap1kBAAAAvtUTUwMAwUaJO97KdkvqiWGxwdAO6o8SYVgAAAAAAAAAAACMGAg5-PjMXONufW8hK_6Ed88udA==",
             "order_id": "05f79ec6fb4143f2ae22d7c449d6b094",
             "source": {  
                "point": [  
                   37.639689099999998,
                   55.735297299999999
                ],
                "short_text": "Озерковская набережная, 48/50с1"
             },
             "status": "finished",
             "surge_coefficient": 1,
             "updated_time": 1505742918
          }
       ]
    }
    

### Допустимые параметры запроса

*   ⋮ __id__ `t: string`     User session id
*    __range__ `t: `     Structure describing a part of an order history to be returned
    *   ⋮ __item_id__ `t: `     An id of a history item serving as boundary. Client requests a list of history items either newer than last known item or older than oldest known item.
        *    __newer_than__ `t: string`     If set, returned items will be stricly older than this id. Either `older_than` or `newer_than` field required
        *    __older_than__ `t: string`     If set, returned items will be stricly newer than this id. Either `older_than` or `newer_than` field required
        *    __results__ `t: integer`     Number of items requested.

### Допустимые параметры ответа

*   ⋮ __items__ `t: array`     ?
    *   ⋮ __created_time__ `t: integer`  `f: int64`   UNIX timestamp of order creation
    *   ⋮ __currency_code__ `t: string`     Code of a currency which an order is nominated in.
    *   ⋮ __destinations__ `t: array`     List of order destinations
        *   ⋮ __point__ `t: array`     Geographical location of an entity, as a longitude-latitude WGS84 coordinates
        *   ⋮ __short_text__ `t: string`     Short point description
    *   ⋮ __final_cost__ `t: string`     Final cost of a ride
    *   ⋮ __item_id__ `t: string`     A unique identifier of a history item
    *   ⋮ __map_image__ `t: string`     URL to a map of a ride
    *   ⋮ __order_id__ `t: string`     An id of an order
    *   ⋮ __source__ `t: `     Address data to display in order history
        *   ⋮ __point__ `t: array`     Geographical location of an entity, as a longitude-latitude WGS84 coordinates
        *   ⋮ __short_text__ `t: string`     Short point description
    *   ⋮ __status__ `t: string` `v: cancelled/finished`    Order status
    *   ⋮ __updated_time__ `t: integer`  `f: int64`   UNIX timestamp of last order update
    *    __display_surge__ `t: boolean`     True вЂ” indicate surge pricing was applied to an order, false otherwise
    *    __rating__ `t: number`     Rating that was set upon order completion, if any
    *    __surge_coefficient__ `t: number`     Surge coefficient which user agreed to

<a name="request_parkdetails"></a>
## parkdetails
### Описание

Информация о тарифах таксопарка.

В `tariffs` у услуг и групп услуг добавлен параметр `id` (такой, что `service_name.<id>` будет совпадать с ключом строки в Танкере).

### Время действия интервала

Задаётся полем `schedule`.

Будни:

    "schedule": {
        "1": [{"start": "09:00", "end": "20:59"}],
        "2": [{"start": "09:00", "end": "20:59"}],
        "3": [{"start": "09:00", "end": "20:59"}],
        "4": [{"start": "09:00", "end": "20:59"}],
        "5": [{"start": "09:00", "end": "20:59"}]
    }

Ночь + выходные:

    "schedule": {
        "1": [{"end": "08:59"}, {"start": "21:00"}],
        "2": [{"end": "08:59"}, {"start": "21:00"}],
        "3": [{"end": "08:59"}, {"start": "21:00"}],
        "4": [{"end": "08:59"}, {"start": "21:00"}],
        "5": [{"end": "08:59"}, {"start": "21:00"}],
        "6": [{"start": "00:00", "end": "23:59"}],
        "7": [{"start": "00:00", "end": "23:59"}]
    }

Праздники и выходные дни:

    "schedule": {
        "holiday": [{"start": "00:00", "end": "23:59"}],
        "6": [{"start": "00:00", "end": "23:59"}],
        "7": [{"start": "00:00", "end": "23:59"}]
    }

**ВАЖНО!**

*   время считается включительно, т.е. `{"start": "10:00", "end": "10:29"}` означает "с 10:00:00 до 10:29:59 включительно"


### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "parkid": "999002"
    }

-

    {
        "parkid": "999002",
        "rating": 4.8,
        "rating_count": 159,
        "tariffs": [
            {
                "intervals": [
                    {
                        "name": "будни", 
                        "price_groups": [
                            {
                                "prices": [
                                    {
                                        "price": "400 руб", 
                                        "id": "taximeter.once_price", 
                                        "name": "Посадка в авто"
                                    }, 
                                    {
                                        "price": "12 руб/мин", 
                                        "id": "taximeter.prepaid", 
                                        "name": "Включено 30 мин, дальше"
                                    }, 
                                    {
                                        "price": "15 руб/км", 
                                        "id": "taximeter.meter_suburb", 
                                        "name": "По области"
                                    }, 
                                    {
                                        "price": "15 руб/км", 
                                        "id": "paid_dispatch.meter_moscow", 
                                        "name": "Подача за МКАД"
                                    }, 
                                    {
                                        "price": "5 мин", 
                                        "id": "free_waiting", 
                                        "name": "Бесплатное ожидание"
                                    }, 
                                    {
                                        "price": "60 руб/мин", 
                                        "id": "paid_waiting", 
                                        "name": "Платное ожидание (не включено в минимальную стоимость!)"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "childchair", 
                                        "name": "Детское кресло или бустер"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "universal", 
                                        "name": "Кузов универсал"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Помощь в переносе багажа, за единицу"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Дополнительное место в салоне для багажа (кроме дамских сумок и пакетов), за единицу"
                                    }, 
                                    {
                                        "price": "250 руб", 
                                        "id": "other", 
                                        "name": "Отказ клиента при поданной машине"
                                    }
                                ], 
                                "comment": "Включенное бесплатное ожидание - 10 минут от контрольного времени. Платное ожидание оплачивается отдельно от минимальной стоимости заказа, в случае превышения 10 минут (отдельно от бесплатных).", 
                                "name": "По городу", 
                                "id": "free_route"
                            }, 
                            {
                                "prices": [
                                    {
                                        "price": "1300 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-Восточный административный округ"
                                    }, 
                                    {
                                        "price": "1300 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-Западный административный округ"
                                    }, 
                                    {
                                        "price": "1350 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-Северный административный округ"
                                    }, 
                                    {
                                        "price": "1300 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-Центральный административный округ"
                                    }, 
                                    {
                                        "price": "1200 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-Южный административный округ"
                                    }, 
                                    {
                                        "price": "1250 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-Восточный административный округ"
                                    }, 
                                    {
                                        "price": "1250 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-Западный административный округ"
                                    }, 
                                    {
                                        "price": "1200 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-Северный административный округ"
                                    }, 
                                    {
                                        "price": "1250 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-Центральный административный округ"
                                    }, 
                                    {
                                        "price": "1350 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-Южный административный округ"
                                    }, 
                                    {
                                        "price": "1100 руб", 
                                        "id": "fixed_route", 
                                        "name": "Восточный административный округ-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "1050 руб", 
                                        "id": "fixed_route", 
                                        "name": "Восточный административный округ-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "1100 руб", 
                                        "id": "fixed_route", 
                                        "name": "Западный административный округ-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "1050 руб", 
                                        "id": "fixed_route", 
                                        "name": "Западный административный округ-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "1150 руб", 
                                        "id": "fixed_route", 
                                        "name": "Северный административный округ-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "1000 руб", 
                                        "id": "fixed_route", 
                                        "name": "Северный административный округ-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "1100 руб", 
                                        "id": "fixed_route", 
                                        "name": "Центральный административный округ-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "1050 руб", 
                                        "id": "fixed_route", 
                                        "name": "Центральный административный округ-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "1000 руб", 
                                        "id": "fixed_route", 
                                        "name": "Южный административный округ-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "1150 руб", 
                                        "id": "fixed_route", 
                                        "name": "Южный административный округ-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "12 руб/мин", 
                                        "id": "taximeter.prepaid", 
                                        "name": "Включено 2 ч, дальше"
                                    }, 
                                    {
                                        "price": "15 руб/км", 
                                        "id": "paid_dispatch.meter_moscow", 
                                        "name": "Подача за МКАД"
                                    }, 
                                    {
                                        "price": "15 руб/км", 
                                        "id": "continue_transfer.meter", 
                                        "name": "Областной тариф"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "childchair", 
                                        "name": "Детское кресло или бустер"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "universal", 
                                        "name": "Кузов универсал"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "other", 
                                        "name": "Встреча с табличкой"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Помощь в переносе багажа, за единицу"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Дополнительное место в салоне для багажа (кроме дамских сумок и пакетов), за единицу"
                                    }
                                ], 
                                "comment": "Бесплатное ожидание при подаче в аэропорт: 30 минут. При встрече в зале аэропорта с табличкой, стоянка оплачивается отдельно клиентом и не включается в стоимость поездки! Если до поездки в аэропорт предшествовал маршрут по городу, либо после встречи следует дополнительный маршрут, стоимость дополнительного маршрута рассчитывается отдельно, исходя из городских тарифов без учета минимальной стоимости поездки. Трансфер в область или из области считается как трансфер до ближайшей из зон: Восточный административный округ, Западный административный округ, Северный административный округ, Центральный административный округ, Южный административный округ, - плюс областной тариф.", 
                                "name": "В/из аэропорта", 
                                "id": "fromto_airport"
                            }, 
                            {
                                "prices": [
                                    {
                                        "price": "1800 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "1800 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "800 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "12 руб/мин", 
                                        "id": "taximeter.prepaid", 
                                        "name": "Включено 3 ч, дальше"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "childchair", 
                                        "name": "Детское кресло или бустер"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "universal", 
                                        "name": "Кузов универсал"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "other", 
                                        "name": "Встреча с табличкой"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Помощь в переносе багажа, за единицу"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Дополнительное место в салоне для багажа (кроме дамских сумок и пакетов), за единицу"
                                    }
                                ], 
                                "comment": "Бесплатное ожидание при подаче в аэропорт: 60 минут. При встрече в зале аэропорта с табличкой, стоянка оплачивается отдельно клиентом и не включается в стоимость поездки!", 
                                "name": "Между аэропортами", 
                                "id": "between_airports"
                            }
                        ], 
                        "schedule": {
                            "1": [
                                {
                                    "start": "09:00", 
                                    "end": "20:59"
                                }
                            ], 
                            "3": [
                                {
                                    "start": "09:00", 
                                    "end": "20:59"
                                }
                            ], 
                            "2": [
                                {
                                    "start": "09:00", 
                                    "end": "20:59"
                                }
                            ], 
                            "5": [
                                {
                                    "start": "09:00", 
                                    "end": "20:59"
                                }
                            ], 
                            "4": [
                                {
                                    "start": "09:00", 
                                    "end": "20:59"
                                }
                            ]
                        }
                    }, 
                    {
                        "name": "ночь", 
                        "price_groups": [
                            {
                                "prices": [
                                    {
                                        "price": "450 руб", 
                                        "id": "taximeter.once_price", 
                                        "name": "Посадка в авто"
                                    }, 
                                    {
                                        "price": "13 руб/мин", 
                                        "id": "taximeter.prepaid", 
                                        "name": "Включено 30 мин, дальше"
                                    }, 
                                    {
                                        "price": "15 руб/км", 
                                        "id": "taximeter.meter_suburb", 
                                        "name": "По области"
                                    }, 
                                    {
                                        "price": "15 руб/км", 
                                        "id": "paid_dispatch.meter_moscow", 
                                        "name": "Подача за МКАД"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "childchair", 
                                        "name": "Детское кресло или бустер"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "universal", 
                                        "name": "Кузов универсал"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Помощь в переносе багажа, за единицу"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Дополнительное место в салоне для багажа (кроме дамских сумок и пакетов), за единицу"
                                    }, 
                                    {
                                        "price": "250 руб", 
                                        "id": "other", 
                                        "name": "Отказ клиента при поданной машине"
                                    }
                                ], 
                                "comment": "Включенное бесплатное ожидание - 10 минут от контрольного времени. Платное ожидание оплачивается отдельно от минимальной стоимости заказа, в случае превышения 10 минут (отдельно от бесплатных).", 
                                "name": "По городу", 
                                "id": "free_route"
                            }, 
                            {
                                "prices": [
                                    {
                                        "price": "1300 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-Восточный административный округ"
                                    }, 
                                    {
                                        "price": "1300 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-Западный административный округ"
                                    }, 
                                    {
                                        "price": "1350 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-Северный административный округ"
                                    }, 
                                    {
                                        "price": "1300 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-Центральный административный округ"
                                    }, 
                                    {
                                        "price": "1200 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-Южный административный округ"
                                    }, 
                                    {
                                        "price": "1250 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-Восточный административный округ"
                                    }, 
                                    {
                                        "price": "1250 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-Западный административный округ"
                                    }, 
                                    {
                                        "price": "1200 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-Северный административный округ"
                                    }, 
                                    {
                                        "price": "1250 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-Центральный административный округ"
                                    }, 
                                    {
                                        "price": "1350 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-Южный административный округ"
                                    }, 
                                    {
                                        "price": "1100 руб", 
                                        "id": "fixed_route", 
                                        "name": "Восточный административный округ-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "1050 руб", 
                                        "id": "fixed_route", 
                                        "name": "Восточный административный округ-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "1100 руб", 
                                        "id": "fixed_route", 
                                        "name": "Западный административный округ-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "1050 руб", 
                                        "id": "fixed_route", 
                                        "name": "Западный административный округ-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "1150 руб", 
                                        "id": "fixed_route", 
                                        "name": "Северный административный округ-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "1000 руб", 
                                        "id": "fixed_route", 
                                        "name": "Северный административный округ-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "1100 руб", 
                                        "id": "fixed_route", 
                                        "name": "Центральный административный округ-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "1050 руб", 
                                        "id": "fixed_route", 
                                        "name": "Центральный административный округ-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "1000 руб", 
                                        "id": "fixed_route", 
                                        "name": "Южный административный округ-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "1150 руб", 
                                        "id": "fixed_route", 
                                        "name": "Южный административный округ-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "13 руб/мин", 
                                        "id": "taximeter.prepaid", 
                                        "name": "Включено 2 ч, дальше"
                                    }, 
                                    {
                                        "price": "15 руб/км", 
                                        "id": "paid_dispatch.meter_moscow", 
                                        "name": "Подача за МКАД"
                                    }, 
                                    {
                                        "price": "15 руб/км", 
                                        "id": "continue_transfer.meter", 
                                        "name": "Областной тариф"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "childchair", 
                                        "name": "Детское кресло или бустер"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "universal", 
                                        "name": "Кузов универсал"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "other", 
                                        "name": "Встреча с табличкой"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Помощь в переносе багажа, за единицу"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Дополнительное место в салоне для багажа (кроме дамских сумок и пакетов), за единицу"
                                    }
                                ], 
                                "comment": "Бесплатное ожидание при подаче в аэропорт: 30 минут. При встрече в зале аэропорта с табличкой, стоянка оплачивается отдельно клиентом и не включается в стоимость поездки! Если до поездки в аэропорт предшествовал маршрут по городу, либо после встречи следует дополнительный маршрут, стоимость дополнительного маршрута рассчитывается отдельно, исходя из городских тарифов без учета минимальной стоимости поездки. Трансфер в область или из области считается как трансфер до ближайшей из зон: Восточный административный округ, Западный административный округ, Северный административный округ, Центральный административный округ, Южный административный округ, - плюс областной тариф.", 
                                "name": "В/из аэропорта", 
                                "id": "fromto_airport"
                            }, 
                            {
                                "prices": [
                                    {
                                        "price": "1800 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "1800 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "800 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "13 руб/мин", 
                                        "id": "taximeter.prepaid", 
                                        "name": "Включено 3 ч, дальше"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "childchair", 
                                        "name": "Детское кресло или бустер"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "universal", 
                                        "name": "Кузов универсал"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "other", 
                                        "name": "Встреча с табличкой"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Помощь в переносе багажа, за единицу"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Дополнительное место в салоне для багажа (кроме дамских сумок и пакетов), за единицу"
                                    }
                                ], 
                                "comment": "Бесплатное ожидание при подаче в аэропорт: 60 минут. При встрече в зале аэропорта с табличкой, стоянка оплачивается отдельно клиентом и не включается в стоимость поездки!", 
                                "name": "Между аэропортами", 
                                "id": "between_airports"
                            }
                        ], 
                        "schedule": {
                            "1": [
                                {
                                    "start": "21:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "3": [
                                {
                                    "start": "00:00", 
                                    "end": "08:59"
                                }, 
                                {
                                    "start": "21:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "2": [
                                {
                                    "start": "00:00", 
                                    "end": "08:59"
                                }, 
                                {
                                    "start": "21:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "5": [
                                {
                                    "start": "00:00", 
                                    "end": "08:59"
                                }
                            ], 
                            "4": [
                                {
                                    "start": "00:00", 
                                    "end": "08:59"
                                }, 
                                {
                                    "start": "21:00", 
                                    "end": "23:59"
                                }
                            ]
                        }
                    }, 
                    {
                        "name": "день ночь выходные праздники", 
                        "price_groups": [
                            {
                                "prices": [
                                    {
                                        "price": "450 руб", 
                                        "id": "taximeter.once_price", 
                                        "name": "Посадка в авто"
                                    }, 
                                    {
                                        "price": "13 руб/мин", 
                                        "id": "taximeter.prepaid", 
                                        "name": "Включено 30 мин, дальше"
                                    }, 
                                    {
                                        "price": "15 руб/км", 
                                        "id": "taximeter.meter_suburb", 
                                        "name": "По области"
                                    }, 
                                    {
                                        "price": "15 руб/км", 
                                        "id": "paid_dispatch.meter_moscow", 
                                        "name": "Подача за МКАД"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "childchair", 
                                        "name": "Детское кресло или бустер"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "universal", 
                                        "name": "Кузов универсал"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Помощь в переносе багажа, за единицу"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Дополнительное место в салоне для багажа (кроме дамских сумок и пакетов), за единицу"
                                    }, 
                                    {
                                        "price": "250 руб", 
                                        "id": "other", 
                                        "name": "Отказ клиента при поданной машине"
                                    }
                                ], 
                                "comment": "Включенное бесплатное ожидание - 10 минут от контрольного времени. Платное ожидание оплачивается отдельно от минимальной стоимости заказа, в случае превышения 10 минут (отдельно от бесплатных).", 
                                "name": "По городу", 
                                "id": "free_route"
                            }, 
                            {
                                "prices": [
                                    {
                                        "price": "1300 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-Восточный административный округ"
                                    }, 
                                    {
                                        "price": "1300 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-Западный административный округ"
                                    }, 
                                    {
                                        "price": "1350 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-Северный административный округ"
                                    }, 
                                    {
                                        "price": "1300 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-Центральный административный округ"
                                    }, 
                                    {
                                        "price": "1200 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-Южный административный округ"
                                    }, 
                                    {
                                        "price": "1250 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-Восточный административный округ"
                                    }, 
                                    {
                                        "price": "1250 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-Западный административный округ"
                                    }, 
                                    {
                                        "price": "1200 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-Северный административный округ"
                                    }, 
                                    {
                                        "price": "1250 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-Центральный административный округ"
                                    }, 
                                    {
                                        "price": "1350 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-Южный административный округ"
                                    }, 
                                    {
                                        "price": "1100 руб", 
                                        "id": "fixed_route", 
                                        "name": "Восточный административный округ-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "1050 руб", 
                                        "id": "fixed_route", 
                                        "name": "Восточный административный округ-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "1100 руб", 
                                        "id": "fixed_route", 
                                        "name": "Западный административный округ-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "1050 руб", 
                                        "id": "fixed_route", 
                                        "name": "Западный административный округ-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "1150 руб", 
                                        "id": "fixed_route", 
                                        "name": "Северный административный округ-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "1000 руб", 
                                        "id": "fixed_route", 
                                        "name": "Северный административный округ-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "1100 руб", 
                                        "id": "fixed_route", 
                                        "name": "Центральный административный округ-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "1050 руб", 
                                        "id": "fixed_route", 
                                        "name": "Центральный административный округ-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "1000 руб", 
                                        "id": "fixed_route", 
                                        "name": "Южный административный округ-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "1150 руб", 
                                        "id": "fixed_route", 
                                        "name": "Южный административный округ-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "13 руб/мин", 
                                        "id": "taximeter.prepaid", 
                                        "name": "Включено 2 ч, дальше"
                                    }, 
                                    {
                                        "price": "15 руб/км", 
                                        "id": "paid_dispatch.meter_moscow", 
                                        "name": "Подача за МКАД"
                                    }, 
                                    {
                                        "price": "15 руб/км", 
                                        "id": "continue_transfer.meter", 
                                        "name": "Областной тариф"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "childchair", 
                                        "name": "Детское кресло или бустер"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "universal", 
                                        "name": "Кузов универсал"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "other", 
                                        "name": "Встреча с табличкой"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Помощь в переносе багажа, за единицу"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Дополнительное место в салоне для багажа (кроме дамских сумок и пакетов), за единицу"
                                    }
                                ], 
                                "comment": "Бесплатное ожидание при подаче в аэропорт: 30 минут. При встрече в зале аэропорта с табличкой, стоянка оплачивается отдельно клиентом и не включается в стоимость поездки! Если до поездки в аэропорт предшествовал маршрут по городу, либо после встречи следует дополнительный маршрут, стоимость дополнительного маршрута рассчитывается отдельно, исходя из городских тарифов без учета минимальной стоимости поездки. Трансфер в область или из области считается как трансфер до ближайшей из зон: Восточный административный округ, Западный административный округ, Северный административный округ, Центральный административный округ, Южный административный округ, - плюс областной тариф.", 
                                "name": "В/из аэропорта", 
                                "id": "fromto_airport"
                            }, 
                            {
                                "prices": [
                                    {
                                        "price": "1800 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "1800 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "800 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "13 руб/мин", 
                                        "id": "taximeter.prepaid", 
                                        "name": "Включено 3 ч, дальше"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "childchair", 
                                        "name": "Детское кресло или бустер"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "universal", 
                                        "name": "Кузов универсал"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "other", 
                                        "name": "Встреча с табличкой"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Помощь в переносе багажа, за единицу"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "other", 
                                        "name": "Дополнительное место в салоне для багажа (кроме дамских сумок и пакетов), за единицу"
                                    }
                                ], 
                                "comment": "Бесплатное ожидание при подаче в аэропорт: 60 минут. При встрече в зале аэропорта с табличкой, стоянка оплачивается отдельно клиентом и не включается в стоимость поездки!", 
                                "name": "Между аэропортами", 
                                "id": "between_airports"
                            }
                        ], 
                        "schedule": {
                            "1": [
                                {
                                    "start": "00:00", 
                                    "end": "08:59"
                                }
                            ], 
                            "holiday": [
                                {
                                    "start": "00:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "5": [
                                {
                                    "start": "21:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "7": [
                                {
                                    "start": "00:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "6": [
                                {
                                    "start": "00:00", 
                                    "end": "23:59"
                                }
                            ]
                        }
                    }
                ], 
                "class": "econom", 
                "name": "Эконом", 
                "id": "1"
            }, 
            {
                "intervals": [
                    {
                        "name": "будни", 
                        "price_groups": [
                            {
                                "prices": [
                                    {
                                        "price": "340 руб", 
                                        "id": "taximeter.once_price", 
                                        "name": "[1] Посадка в авто"
                                    }, 
                                    {
                                        "price": "14 руб/мин", 
                                        "id": "taximeter.prepaid", 
                                        "name": "[1] Включено 20 мин, дальше"
                                    }, 
                                    {
                                        "price": "30 руб/км", 
                                        "id": "taximeter.meter_city", 
                                        "name": "[2] По городу"
                                    }, 
                                    {
                                        "price": "9 руб/км", 
                                        "id": "taximeter.meter_mkad", 
                                        "name": "По МКАД"
                                    }, 
                                    {
                                        "price": "20 руб/км", 
                                        "id": "taximeter.meter_suburb", 
                                        "name": "По области"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Белорусский вокзал)"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Казанский вокзал)"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Киевский вокзал)"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Курский вокзал)"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Ленинградский вокзал)"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Павелецкий вокзал)"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Рижский вокзал)"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Савёловский вокзал)"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Ярославский вокзал)"
                                    }, 
                                    {
                                        "price": "5 руб/км", 
                                        "id": "paid_dispatch.meter_moscow", 
                                        "name": "Подача за МКАД"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "paid_dispatch.min_price_moscow", 
                                        "name": "Минимальная стоимость подачи за МКАД"
                                    }, 
                                    {
                                        "price": "100 руб", 
                                        "id": "childchair", 
                                        "name": "Детское кресло или бустер"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "universal", 
                                        "name": "Кузов универсал"
                                    }, 
                                    {
                                        "price": "100 руб", 
                                        "id": "other", 
                                        "name": "Дополнительное место в салоне для багажа, за единицу"
                                    }, 
                                    {
                                        "price": "340 руб", 
                                        "id": "other", 
                                        "name": "Отказ клиента при поданной машине"
                                    }
                                ], 
                                "comment": "Предоставляется 5 минут бесплатного ожидания. Оплата за парковку на платных стоянках по согласованию с клиентом осуществляется отдельно от оплаты услуг такси. Животные в салоне такси могут перевозиться только в случае наличия коврика и корзины (контейнера). Оплата по счётчику производится на основании наибольшей цены из: [1], [2].", 
                                "name": "По городу", 
                                "id": "free_route"
                            }, 
                            {
                                "prices": [
                                    {
                                        "price": "1350 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-Центральный административный округ"
                                    }, 
                                    {
                                        "price": "1150 руб", 
                                        "id": "fixed_route", 
                                        "name": "Центральный административный округ-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "14 руб/мин", 
                                        "id": "taximeter.prepaid", 
                                        "name": "Включено 2 ч, дальше"
                                    }, 
                                    {
                                        "price": "5 руб/км", 
                                        "id": "paid_dispatch.meter_moscow", 
                                        "name": "Подача за МКАД"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "paid_dispatch.min_price_moscow", 
                                        "name": "Минимальная стоимость подачи за МКАД"
                                    }, 
                                    {
                                        "price": "20 руб/км", 
                                        "id": "continue_transfer.meter", 
                                        "name": "Областной тариф"
                                    }, 
                                    {
                                        "price": "100 руб", 
                                        "id": "childchair", 
                                        "name": "Детское кресло или бустер"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "universal", 
                                        "name": "Кузов универсал"
                                    }, 
                                    {
                                        "price": "500 руб", 
                                        "id": "other", 
                                        "name": "Отказ клиента при поданной машине"
                                    }
                                ], 
                                "comment": "В стоимость встречи в аэропорту входит 30 мин. бесплатного ожидания. При трансферах из аэропорта в аэропорт время бесплатного ожидания такси составляет 1 час. В случае заезда стоимость рассчитывается как две поездки - городская и в аэропорт. При попутных остановках, по требованию пассажира, ожидание тарифицируется поминутно. Трансфер в область или из области считается как трансфер до ближайшей из зон: Центральный административный округ, - плюс областной тариф.", 
                                "name": "В/из аэропорта", 
                                "id": "fromto_airport"
                            }
                        ], 
                        "schedule": {
                            "1": [
                                {
                                    "start": "09:00", 
                                    "end": "20:59"
                                }
                            ], 
                            "3": [
                                {
                                    "start": "09:00", 
                                    "end": "20:59"
                                }
                            ], 
                            "2": [
                                {
                                    "start": "09:00", 
                                    "end": "20:59"
                                }
                            ], 
                            "5": [
                                {
                                    "start": "09:00", 
                                    "end": "20:59"
                                }
                            ], 
                            "4": [
                                {
                                    "start": "09:00", 
                                    "end": "20:59"
                                }
                            ]
                        }
                    }, 
                    {
                        "name": "день ночь выходные праздники", 
                        "price_groups": [
                            {
                                "prices": [
                                    {
                                        "price": "390 руб", 
                                        "id": "taximeter.once_price", 
                                        "name": "[1] Посадка в авто"
                                    }, 
                                    {
                                        "price": "15 руб/мин", 
                                        "id": "taximeter.prepaid", 
                                        "name": "[1] Включено 20 мин, дальше"
                                    }, 
                                    {
                                        "price": "30 руб/км", 
                                        "id": "taximeter.meter_city", 
                                        "name": "[2] По городу"
                                    }, 
                                    {
                                        "price": "9 руб/км", 
                                        "id": "taximeter.meter_mkad", 
                                        "name": "По МКАД"
                                    }, 
                                    {
                                        "price": "20 руб/км", 
                                        "id": "taximeter.meter_suburb", 
                                        "name": "По области"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Белорусский вокзал)"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Казанский вокзал)"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Киевский вокзал)"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Курский вокзал)"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Ленинградский вокзал)"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Павелецкий вокзал)"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Рижский вокзал)"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Савёловский вокзал)"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "paid_dispatch.other", 
                                        "name": "Подача (Ярославский вокзал)"
                                    }, 
                                    {
                                        "price": "5 руб/км", 
                                        "id": "paid_dispatch.meter_moscow", 
                                        "name": "Подача за МКАД"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "paid_dispatch.min_price_moscow", 
                                        "name": "Минимальная стоимость подачи за МКАД"
                                    }, 
                                    {
                                        "price": "100 руб", 
                                        "id": "childchair", 
                                        "name": "Детское кресло или бустер"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "universal", 
                                        "name": "Кузов универсал"
                                    }, 
                                    {
                                        "price": "100 руб", 
                                        "id": "other", 
                                        "name": "Дополнительное место в салоне для багажа, за единицу"
                                    }, 
                                    {
                                        "price": "390 руб", 
                                        "id": "other", 
                                        "name": "Отказ клиента при поданной машине"
                                    }
                                ], 
                                "comment": "Предоставляется 5 минут бесплатного ожидания. Оплата за парковку на платных стоянках по согласованию с клиентом осуществляется отдельно от оплаты услуг такси. Животные в салоне такси могут перевозиться только в случае наличия коврика и корзины (контейнера). Оплата по счётчику производится на основании наибольшей цены из: [1], [2].", 
                                "name": "По городу", 
                                "id": "free_route"
                            }, 
                            {
                                "prices": [
                                    {
                                        "price": "1350 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-Центральный административный округ"
                                    }, 
                                    {
                                        "price": "1150 руб", 
                                        "id": "fixed_route", 
                                        "name": "Центральный административный округ-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "15 руб/мин", 
                                        "id": "taximeter.prepaid", 
                                        "name": "Включено 2 ч, дальше"
                                    }, 
                                    {
                                        "price": "5 руб/км", 
                                        "id": "paid_dispatch.meter_moscow", 
                                        "name": "Подача за МКАД"
                                    }, 
                                    {
                                        "price": "50 руб", 
                                        "id": "paid_dispatch.min_price_moscow", 
                                        "name": "Минимальная стоимость подачи за МКАД"
                                    }, 
                                    {
                                        "price": "20 руб/км", 
                                        "id": "continue_transfer.meter", 
                                        "name": "Областной тариф"
                                    }, 
                                    {
                                        "price": "100 руб", 
                                        "id": "childchair", 
                                        "name": "Детское кресло или бустер"
                                    }, 
                                    {
                                        "price": "200 руб", 
                                        "id": "universal", 
                                        "name": "Кузов универсал"
                                    }, 
                                    {
                                        "price": "500 руб", 
                                        "id": "other", 
                                        "name": "Отказ клиента при поданной машине"
                                    }
                                ], 
                                "comment": "В стоимость встречи в аэропорту входит 30 мин. бесплатного ожидания. При трансферах из аэропорта в аэропорт время бесплатного ожидания такси составляет 1 час. В случае заезда стоимость рассчитывается как две поездки - городская и в аэропорт. При попутных остановках, по требованию пассажира, ожидание тарифицируется поминутно. Трансфер в область или из области считается как трансфер до ближайшей из зон: Центральный административный округ, - плюс областной тариф.", 
                                "name": "В/из аэропорта", 
                                "id": "fromto_airport"
                            }
                        ], 
                        "schedule": {
                            "1": [
                                {
                                    "start": "00:00", 
                                    "end": "08:59"
                                }, 
                                {
                                    "start": "21:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "3": [
                                {
                                    "start": "00:00", 
                                    "end": "08:59"
                                }, 
                                {
                                    "start": "21:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "2": [
                                {
                                    "start": "00:00", 
                                    "end": "08:59"
                                }, 
                                {
                                    "start": "21:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "5": [
                                {
                                    "start": "00:00", 
                                    "end": "08:59"
                                }, 
                                {
                                    "start": "21:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "4": [
                                {
                                    "start": "00:00", 
                                    "end": "08:59"
                                }, 
                                {
                                    "start": "21:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "7": [
                                {
                                    "start": "00:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "6": [
                                {
                                    "start": "00:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "holiday": [
                                {
                                    "start": "00:00", 
                                    "end": "23:59"
                                }
                            ]
                        }
                    }
                ], 
                "class": "business", 
                "name": "Комфорт", 
                "id": "2"
            }, 
            {
                "intervals": [
                    {
                        "name": "день ночь выходные праздники", 
                        "price_groups": [
                            {
                                "prices": [
                                    {
                                        "price": "750 руб", 
                                        "id": "taximeter.once_price", 
                                        "name": "Посадка в авто (при времени поездки меньше чем 3 ч)"
                                    }, 
                                    {
                                        "price": "25 руб/мин", 
                                        "id": "taximeter.prepaid_city", 
                                        "name": "По городу - включено 30 мин, дальше (при времени поездки меньше чем 3 ч)"
                                    }, 
                                    {
                                        "price": "50 руб/мин", 
                                        "id": "taximeter.prepaid_suburb", 
                                        "name": "По области - включено 15 мин, дальше (при времени поездки меньше чем 3 ч)"
                                    }, 
                                    {
                                        "price": "750 руб", 
                                        "id": "taximeter.once_price", 
                                        "name": "Посадка в авто (при времени поездки больше чем 3 ч)"
                                    }, 
                                    {
                                        "price": "15 руб/мин", 
                                        "id": "taximeter.prepaid_city", 
                                        "name": "По городу - включено 30 мин, дальше (при времени поездки больше чем 3 ч)"
                                    }, 
                                    {
                                        "price": "30 руб/мин", 
                                        "id": "taximeter.prepaid_suburb", 
                                        "name": "По области - включено 15 мин, дальше (при времени поездки больше чем 3 ч)"
                                    }, 
                                    {
                                        "price": "750 руб", 
                                        "id": "other", 
                                        "name": "Штраф при отмене заказа внутри МКАД менее чем за 30 минут"
                                    }, 
                                    {
                                        "price": "750 руб", 
                                        "id": "other", 
                                        "name": "Штраф при отмене заказа за МКАД менее чем за 60 минут"
                                    }, 
                                    {
                                        "price": "1000 руб", 
                                        "id": "other", 
                                        "name": "Персональный водитель (авто без символики)"
                                    }
                                ], 
                                "comment": "Стоимость ожидания - 25 руб/мин. Если поездка длится более 3-х часов, на последующее время действует комплимент-тариф: 15 руб./мин. заказ по Москве, 30 руб./мин. за пределами МКАД. При условии предварительного заказа 10 часов - 9 000 рублей, далее 15 руб./мин.", 
                                "name": "По городу", 
                                "id": "free_route"
                            }, 
                            {
                                "prices": [
                                    {
                                        "price": "2500 руб", 
                                        "id": "fixed_route", 
                                        "name": "город-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "2500 руб", 
                                        "id": "fixed_route", 
                                        "name": "город-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "2500 руб", 
                                        "id": "fixed_route", 
                                        "name": "область-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "2500 руб", 
                                        "id": "fixed_route", 
                                        "name": "область-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "50 руб/мин", 
                                        "id": "taximeter.meter_suburb", 
                                        "name": "По области (при удалённости от города больше чем 10 км)"
                                    }, 
                                    {
                                        "price": "750 руб", 
                                        "id": "other", 
                                        "name": "Штраф при отмене заказа менее чем за 30 минут"
                                    }, 
                                    {
                                        "price": "2000 руб", 
                                        "id": "other", 
                                        "name": "Багажник для лыж"
                                    }
                                ], 
                                "comment": "30 минут бесплатного ожидания. Стоимость дальнейшего ожидания – 25 руб./мин. Действует в пределах 10 км от МКАД.", 
                                "name": "В аэропорт", 
                                "id": "to_airport"
                            }, 
                            {
                                "prices": [
                                    {
                                        "price": "3200 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "2500 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-город"
                                    }, 
                                    {
                                        "price": "2500 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Домодедово-область"
                                    }, 
                                    {
                                        "price": "3200 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-аэропорт Домодедово"
                                    }, 
                                    {
                                        "price": "2500 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-аэропорт Шереметьево"
                                    }, 
                                    {
                                        "price": "2500 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-город"
                                    }, 
                                    {
                                        "price": "2500 руб", 
                                        "id": "fixed_route", 
                                        "name": "аэропорт Шереметьево-область"
                                    }, 
                                    {
                                        "price": "2500 руб", 
                                        "id": "other", 
                                        "name": "Штраф при отмене заказа менее чем за 60 минут"
                                    }, 
                                    {
                                        "price": "2000 руб", 
                                        "id": "other", 
                                        "name": "Багажник для лыж"
                                    }
                                ], 
                                "comment": "60 минут бесплатного ожидания. Стоимость дальнейшего ожидания – 25 руб./мин. Действует в пределах 10 км от МКАД.", 
                                "name": "Из аэропорта", 
                                "id": "from_airport"
                            }
                        ], 
                        "schedule": {
                            "1": [
                                {
                                    "start": "00:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "3": [
                                {
                                    "start": "00:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "2": [
                                {
                                    "start": "00:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "5": [
                                {
                                    "start": "00:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "4": [
                                {
                                    "start": "00:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "7": [
                                {
                                    "start": "00:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "6": [
                                {
                                    "start": "00:00", 
                                    "end": "23:59"
                                }
                            ], 
                            "holiday": [
                                {
                                    "start": "00:00", 
                                    "end": "23:59"
                                }
                            ]
                        }
                    }
                ], 
                "class": "vip", 
                "name": "Бизнес", 
                "id": "3"
            }
        ], 
        "type": "taxipark",
        "name": "Аист",
        "phone": "+74950000002",
        "legal_address": "Street",
        "long_name": "Organization",
        "ogrn": ""
    }

### Допустимые параметры запроса

*   ⋮ __parkid__ `t: string`     идентификатор таксопарка
*    __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __name__ `t: string`     название таксопарка
*   ⋮ __parkid__ `t: string`     идентификатор таксопарка
*   ⋮ __phone__ `t: phone`     номер телефона таксопарка
    *   ⋮ __response__ `t: phone`     объект ответа целиком
*   ⋮ __tariffs__ `t: array`     список тарифов таксопарка
    *   ⋮ __id__ `t: string`     идентификатор тарифа (уникален в пределах таксопарка)
    *   ⋮ __intervals__ `t: array`     временные интервалы
        *   ⋮ __id__ `t: string`     id интервала из МРТ
        *   ⋮ __name__ `t: string`     название интервала
        *   ⋮ __price_groups__ `t: array`     информация, разбитая по группам
            *   ⋮ __name__ `t: string`     название группы
            *   ⋮ __prices__ `t: array`     описание цен
                *   ⋮ __name__ `t: string`     наименование услуги
                *   ⋮ __price__ `t: string`     стоимость услуги
                *    __id__ `t: string`     id услуги
            *    __comment__ `t: string`     комментарий
            *    __id__ `t: string`     id группы услуг
        *   ⋮ __schedule__ `t: schedule`     время действия интервала
            *   ⋮ __response__ `t: schedule`     объект ответа целиком
    *   ⋮ __name__ `t: string`     название тарифа
    *    __class__ `t: tariff_class`     категория тарифа
        *   ⋮ __response__ `t: tariff_class`     объект ответа целиком
*   ⋮ __type__ `t: ` `v: taxipark/dispatch`    таксопарк или диспетчерская
*    __legal_address__ `t: string`     юридический адрес
*    __long_name__ `t: string`     полное наименование организации
*    __ogrn__ `t: string`     ОГРН
*    __rating__ `t: number`     средний рейтинг таксопарка
*    __rating_count__ `t: integer`     число голосов, на которых основан рейтинг

<a name="request_paymentmethods"></a>
## paymentmethods
### Описание

Получение информации о возможных способах оплаты у пользователя.
Новые клиенты должны использовать метод `/paymentmethods` вместо
метода `/cards`, потому что `/paymentmethods` возвращает также информацию
о корпоративных счетах (а в будущем и о других способах оплаты, когда они
появятся)

Сейчас поддерживаются следующие способы оплаты:
* карта (`"card"`)
* корпоративный счет (`"corp"`)

Oauth-токен в заголовке `Authorization: Bearer TOKEN` обязателен. Перед
запросом необходимо сходить в `launch` с тем же токеном, привязав номер
телефона к устройству.

Возможные ошибки и рекомендации по их интерпретации:

  * `406 Not Acceptable`, `UNKNOWN_USER`: пользователь неизвестен;
    необходимо предварительно сделать запрос в launch
  * `401 Unauthorized`, `INVALID_TOKEN`: токен инвалидирован; необходимо
    получить новый токен и сделать запрос в launch со обновлённым
    токеном
  * `406 Not Acceptable`, `MISSING_TOKEN`: токен не передан
  * `406 Not Acceptable`, неизвестный код ошибки; рекомендуется
    отобразить сообщение об ошибке пользователю (поле `error.text`) и
    вернуться на главный экран

### Пример

    {
        "id": "1234567890abcdefghijkl0987654321"
    }

-

    {
        "card": {
            "available_cards": [
                {
                    "id": "card-x7777",
                    "system": "VISA",
                    "number": "401922****1234",
                    "currency": "RUB",
                    "busy": false,
                    "usable": true
                }
            ],
            "payment_available": true,
        },
        
        "corp": {
            "available_accounts": [
                {
                    "id": "some_payment_method_id"
                    "name": "some name",
                    "money_spent": 1340.0,
                    "money_limit": 3000.0,
                    "money_left": 1660.0,
                    "currency": "RUB",
                    "description": "Осталось 1660 руб. из 3000 руб.",
                    "cost_center": "users' default cost center"
                }
            ],
            "payment_available": true
        }
    }

### Допустимые параметры запроса

*    __format_currency__ `t: boolean`      если передан, то в ответе передаем валюты в определенном формате
*    __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа


<a name="request_paymentstatuses"></a>
## paymentstatuses
### Описание

Получение списка оплат по заказам или информация о проведении статуса
оплаты по конкретному заказу.

Для получения списка оплат по заказам необходимо передать в `filter`
типы отображаемых заказов:

* `"debt"` - неоплаченные заказы
* `"need_cvn"` - заказы, платежи по которым требуют ввода CXN
* `"need_accept"` - заказы, требующие подтверждения стоимости поездки
* `"can_be_paid_by_card"` - заказы, которые можно оплатить картой

Способы оплаты заказов зависят от статуса `payment.status` и флагов
`payment.need_cvn`. Возможные значения `payment.status`:

* `"debt"` - заказ не оплачен
* `"cash"` - заказ должен быть оплачен наличными (но можно попробовать
  оплатить картой при наличии поля `can_be_paid_by_card`)
* `"processing"` - платёж в процессе обработки
* `"paid"` - заказ успешно оплачен картой

При наличии флага `payment.need_accept` перед оплатой необходимо
спросить у пользователя, согласен ли он со стоимостью поездки. Если нет,
рекомендуется показывать телефон службы поддержки. Отсутствующее (или
установленное в `false`) поле `can_be_paid_by_card` означает, что заказ
или уже оплачен, или не может быть оплачен картой.

Процедура оплаты заказов:

1. Выбираем заказ из списка.
2. Инициируем запрос на оплату `/3.0/payorder`.
3. Запрашиваем каждые 5 секунд `/3.0/paymentstatuses`, передавая в
  `orderid` идентификатор выбранного в п.1 заказа.
4. При установленном флаге `payment.need_accept` необходимо дождаться
  идентификатора транзакции `payment.trust_payment_id`, который следует
  передать в Биллинг (см. ниже) вместе с CVN, введённым пользователем.
5. При получении статуса `"debt"` (или `"cash"`, если заказ с наличными
не удалось оплатить картой) можно предложить пользователю   повторить
процедуру оплаты.
6. При получении статуса `"paid"` необходимо сообщить об успешно
  проведённом платеже.

API Биллинга для передачи CVN и идентификатора транзакации:
https://beta.wiki.yandex-team.ru/Balance/Simple/JSON/#supplypaymentdata.

**ВАЖНО! Запрос в /3.0/payorder трактуется сервером как согласие клиента
со стоимостью заказа!**


### Пример получения списка заказов

    {
        "id": "1234567890abcdefghijkl0987654321",
        "filter": ["debt", "need_accept", "need_cvn", "can_be_paid_by_card"]
    }

    -

    {
        "cards": [{
            "number": "****4444",
            "id": "card-96061800",
            "system": "MasterCard"
        }],
        "orders": [{
            "orderid": "1f562ab534d04b79ac4cd1b858b2793a",
            "services": [{
                "cost": 540,
                "type": "ride"
            },
            {
                "cost": 0,
                "type": "tips"
            }],
            "payment": {
                "status": "cash",
                "trust_payment_id": null,
                "need_accept": false,
                "need_cvn": true,
                "cardid": "card-96061800"
            },
            "can_be_paid_by_card": true
        }]
    }


### Пример оплаты заказа с вводом CVN

Запрашиваем /3.0/payorder:

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1f562ab534d04b79ac4cd1b858b2793a",
        "cardid": "card-NNNNNNN"
    }

    -

    {}

Дожидаемся `trust_payment_id` в ответе `/3.0/paymentstatuses`:

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1f562ab534d04b79ac4cd1b858b2793a"
    }

    -

    {
        "cards": [{
            "number": "****4444",
            "id": "card-96061800",
            "system": "MasterCard"
        }],
        "orders": [{
            "orderid": "1f562ab534d04b79ac4cd1b858b2793a",
            "services": [{
                "cost": 540,
                "type": "ride"
            },
            {
                "cost": 0,
                "type": "tips"
            }],
            "payment": {
                "status": "processing",
                "trust_payment_id": "55522fae4fe2b153a82a0b3e",
                "need_accept": false,
                "need_cvn": true,
                "cardid": "card-96061800"
            },
            "can_be_paid_by_card": true
        }]
    }

Передаём в Биллинг идентификатор транзакции и CVN:

    {
        "params": {
            "token": "SUPERSECRET",
            "trust_payment_id": "55522fae4fe2b153a82a0b3e",
            "cvn": "300"
        }
    }

    -

    {
        "status": "success"
    }

Дожидаемся результат, запрашивая `/3.0/paymentstatuses`:

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1f562ab534d04b79ac4cd1b858b2793a"
    }

    -

    {
        "cards": [{
            "number": "****4444",
            "id": "card-96061800",
            "system": "MasterCard"
        }],
        "orders": [{
            "orderid": "1f562ab534d04b79ac4cd1b858b2793a",
            "services": [{
                "cost": 540,
                "type": "ride"
            },
            {
                "cost": 0,
                "type": "tips"
            }],
            "payment": {
                "status": "paid",
                "trust_payment_id": null,
                "need_accept": false,
                "need_cvn": false,
                "cardid": "card-96061800"
            }
        }]
    }

### Допустимые параметры запроса

*    __filter__ `t: payment_statuses_filter`     типы платежей, которые необходимо отразить
    *   ⋮ __response__ `t: payment_statuses_filter`     объект ответа целиком
*    __format_currency__ `t: boolean`      если передан, то в ответе передаем валюты в определенном формате
*    __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __orderid__ `t: uuid4`     идентификатор заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __cards__ `t: array`     список карт, использующихся в оплате заказов из списка orders
    *   ⋮ __id__ `t: string`     id способа оплаты для передачи в заказ
    *   ⋮ __number__ `t: string`     номер карты (начало замаскировано звездочками)
    *   ⋮ __system__ `t: string`     платежная система карты (VISA, MasterCard)
*   ⋮ __orders__ `t: array`     ?

<a name="request_payorder"></a>
## payorder
### Описание

Инициирование процесса оплаты картой.

При получении запроса сервер инициирует процесс оплаты заказа картой. В
запросе в обязательном порядке должен передаваться идентификатор карты,
которую клиент желает использовать для оплаты.

Если всё хорошо, сервер вернёт пустой ответ `{}`.

Если карта недоступна или некорректна, вернётся ошибка `406` с причиной
`UNKNOWN_CARD` или `INVALID_CARD` соответственно:

    {
        "error": {
            "code": "UNKNOWN_CARD",
            "text": "Карта не привязана к аккаунту"
        }
    }

Если оплата картой уже невозможна, сервер вернёт код ошибки `410`.

Пример работы с ручкой см. в описании работы в `/3.0/paymentstatuses`.

### Допустимые параметры запроса

*   ⋮ __cardid__ `t: string`  `f: payment_id`   идентификатор карты, которая будет использоваться для оплаты
*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __orderid__ `t: uuid4`     идентификатор заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __type__ `t: payment_method`     ?
    *   ⋮ __response__ `t: payment_method`     объект ответа целиком

### Допустимые параметры ответа


<a name="request_pickuppoints"></a>
## pickuppoints
### Описание
https://wiki.yandex-team.ru/taxi/mobile/pickuppoints/

### Пример
curl -v -H "Content-Type: application/json" -X POST -d '{"dx": 10, "ll": [37.589366, 55.734238]}' "http://tc.tst.mobile.yandex.net/3.0/pickuppoints"

    {
        "points": [
            {
                "geometry": [
                    37.58935025973962,
                    55.73423185102005
                ],
                "id": "fbb68f7f0391464092812bcef420a829_2"
            },
            {
                "geometry": [
                    37.590787,
                    55.73334
                ],
                "id": "15d12b944e6a4a3ba4f9582acd6f538f_2"
            },
            {
                "geometry": [
                    37.58775702758494,
                    55.73333288307965
                ],
                "id": "fbb68f7f0391464092812bcef420a829_1"
            },
            {
                "geometry": [
                    37.587707,
                    55.733307
                ],
                "id": "15d12b944e6a4a3ba4f9582acd6f538f_0"
            },
            {
                "geometry": [
                    37.58672,
                    55.733972
                ],
                "id": "fbb68f7f0391464092812bcef420a829_0"
            }
        ]
    }
### Допустимые параметры запроса

*   ⋮ __dx__ `t: number`     точность определения координат пользователя в метрах
*   ⋮ __ll__ `t: point`     координаты пользователя
    *   ⋮ __response__ `t: point`     объект ответа целиком

### Допустимые параметры ответа

*    __groups__ `t: array`     Группы точек посадки
    *   ⋮ __id__ `t: string`     ?
    *   ⋮ __name__ `t: string`     ?
    *   ⋮ __points__ `t: array`     Точки из группы
        *   ⋮ __distance__ `t: number`     ?
        *   ⋮ __geometry__ `t: point`     ?
            *   ⋮ __response__ `t: point`     объект ответа целиком
        *   ⋮ __name__ `t: string`     название точки
    *    __zones__ `t: array`     Зоны из группы
        *   ⋮ __geometry__ `t: array`     ?
            *   ⋮ __response__ `t: point`     объект ответа целиком
        *   ⋮ __name__ `t: string`     название зоны

<a name="request_pricecat"></a>
## pricecat
### Описание

Информация о работающих в городе таксопарках.


### Важно

Сервер Я.Такси сортирует таксопарки по соотношению рейтинг/цена. Клиенты не должны применять какие-либо дополнительные методы сортировки.

Поле `schedule` подробно описано в `parkdetails`.

Ручка поддерживает пагинацию. Если все результаты не поместились в один ответ, то в ответе будет поле next, где будет указан номер следующей страницы.
Чтобы получить страницу с номером N, нужно сделать запрос /pricecat?page=N (нумерация страниц начинается с нуля).
Если сделан запрос без указания номера страницы (то есть /pricecat), то в ответ всегда будет только первая страница результатов, БЕЗ поля next, даже если есть результаты на следующей страницы. (сделано из соображений совместмости со старыми клиентам, см. https://st.yandex-team.ru/TAXIBACKEND-6942 )
По умолчанию на странице 1000 таксопарков.


### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "city": "Москва"
    }

-

    {
        "parks": [{
            "parkid": "999003",
            "rating_count": 19,
            "rating": 5.0,
            "name": "Опа!",
            "phone": "+79999999999,1234",
            "forwarding_phone": "+79999999999",
            "forwarding_ext": "1234",
            "tariffs_url": "https://m.taxi.yandex.ru/park-tariff/?parkid=999003",
            "tariffs": [{
                "intervals": [{
                    "description": "от 199 руб",
                    "schedule": {
                        "1": [{
                            "start": "08:00",
                            "end": "20:59"
                        }],
                        "3": [{
                            "start": "08:00",
                            "end": "20:59"
                        }],
                        "2": [{
                            "start": "08:00",
                            "end": "20:59"
                        }],
                        "4": [{
                            "start": "08:00",
                            "end": "20:59"
                        }],
                        "7": [{
                            "start": "08:00",
                            "end": "20:59"
                        }]
                    }
                }, {
                    "description": "от 249 руб",
                        "schedule": {
                            "1": [{
                                "start": "00:00",
                                "end": "07:59"
                            }, {
                                "start": "21:00",
                                "end": "23:59"
                            }],
                            "3": [{
                                "start": "00:00",
                                "end": "07:59"
                            }, {
                                "start": "21:00",
                                "end": "23:59"
                            }],
                            "2": [{
                                "start": "00:00",
                                "end": "07:59"
                            }, {
                                "start": "21:00",
                                "end": "23:59"
                            }],
                            "5": [{
                                "start": "00:00",
                                "end": "23:59"
                            }],
                            "4": [{
                                "start": "00:00",
                                "end": "07:59"
                            }, {
                                "start": "21:00",
                                "end": "23:59"
                            }],
                            "7": [{
                                "start": "00:00",
                                "end": "07:59"
                            }, {
                                "start": "21:00",
                                "end": "23:59"
                            }],
                            "6": [{
                                "start": "00:00",
                                "end": "23:59"
                            }],
                            "holiday": [{
                                "start": "00:00",
                                "end": "23:59"
                            }]
                        }
                }],
                    "id": "1",
                    "class": "econom"
            }, {
                "intervals": [{...}],
                    "id": "2",
                    "class": "business"
            }, {
                "intervals": [{...}],
                    "id": "3",
                    "class": "vip"
            }],
            "type": "dispatch"
        }, {
            "parkid": "999002",
            "tariffs": [...],
            "tariffs_url": "https://m.taxi.yandex.ru/park-tariff/?parkid=999002",
            "type": "taxipark",
            "name": "Аист",
            "phone": "+74950000002"
        }]
    }

### Допустимые параметры запроса

*    __city__ `t: city`     город, в котором принимаем заказы
    *   ⋮ __response__ `t: city`     объект ответа целиком
*    __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __zone_name__ `t: string`     название зоны

### Допустимые параметры ответа

*   ⋮ __parks__ `t: array`     список таксопарков города с краткой информацией о тарифах
    *   ⋮ __name__ `t: string`     название таксопарка
    *   ⋮ __parkid__ `t: string`     идентификатор таксопарка
    *   ⋮ __phone__ `t: phone`     номер телефона таксопарка
        *   ⋮ __response__ `t: phone`     объект ответа целиком
    *   ⋮ __tariffs__ `t: array`     минимальные цены в тарифах таксопарка
        *   ⋮ __class__ `t: tariff_class`     категория тарифа
            *   ⋮ __response__ `t: tariff_class`     объект ответа целиком
        *   ⋮ __id__ `t: string`     идентификатор тарифа (уникален в пределах таксопарка)
        *   ⋮ __intervals__ `t: array`     временные интервалы
            *   ⋮ __description__ `t: string`     информация о минималке
            *   ⋮ __schedule__ `t: schedule`     время действия интервала
                *   ⋮ __response__ `t: schedule`     объект ответа целиком
    *   ⋮ __tariffs_url__ `t: string`     ссылка на страницу с тарифами таксопарка
    *   ⋮ __type__ `t: ` `v: taxipark/dispatch`    тип парка, таксопарк или диспетчерская
    *    __rating__ `t: number`     средний рейтинг таксопарка
    *    __rating_count__ `t: integer`     число голосов, на которых основан рейтинг
*    __next__ `t: integer`     номер следующей страницы списка таксопарков. Поле будет только если следующая страница существует

<a name="request_promotions"></a>
## promotions
### Описание

Информация о доступных для пользователя промо-акциях. На вход требует список
идентификаторов поддерживаемых промо-акций, для того, чтобы сделать выбор.

Ручка требует id пользователя (по факту сейчас логин не нужен,
но в будущем поможет делать персонификацию акций).

Есть поддержка кэширования, как с помощью механизмов `If-Modified-Since`
так и с помощью `ETag`.

Кроме того, если в запросе присутствует поле `fullscreen_banner`, ручка вернет полноэкранные баннеры,
действующие в данный момент, если таковые имеются. Для получения баннеров необходимо:

* Передать в `id` идентификатор пользователя (для ведения статистики показов на стороне бекенда)
* Передать в запросе параметр `fullscreen_banner`, представляющий собой объект с двумя ключами:
  * `size_hint` - требуемый размер изображения (семантику см. в ручке `tariffs`).
  * `banners_seen` - массив id баннеров, которые уже видел данный клиент (для ведения статистики на стороне бекенда,
      не влияет на то, какой список баннеров возвратит ручка).
      
В ответе возвращается список активных промоакций `active_promotions` с информацией по ним

* `name`  - название/идентификатор акции
* `cities` - города, в которых действует акция
* `zones` - геозоны, в которых действует акция
* `image_tags` - теги (а не сслыки) картинок,
которые могут понадобиться при отображении пользователю диалогов по промоакции. 
Может использоваться для предварительной загрузки изображений
* `action` - действие, связанное с промо-акцией, объект содержащий поля:
  * `deeplink` - диплинк, ссылка.
  * `target` - опциональное поле, возможные значения: webview.

В ответе также будет возвращен параметр `fullscreen_banner`, представляющий собой список объектов со следующими полями:
* `id` - идентификатор баннера. Строка непрозрачного для клиента  содержания, которую можно отправить
    на бекенд в `banners_seen`.
* `cities` - массив городов, в которых нужно показывать баннер. Если отстутсвует, баннер действует во всех городах.
* `caption` - локализованный заголовок баннера.
* `text` - локализованный текст баннера.
* `image`, `background`, `logo` - объект-изображение (см. `tariffs`).
* `widgets` - объект, определяющий виджеты (кнопки), которые должны быть на баннере:
  * `close_button` - булево значение. Если присутствует и равно `true`, нужен "крестик".
  * `menu_button` - булево значение. Если присутствует и равно `true`, нужна кнопка меню.
  * `action_button` - объект. Если присутствует, содержит локализованный текст кнопки внизу баннера (`label`)
      и ее диплинк (`deeplink`). В противном случае кнопку отображать не надо.
      Если содержит поле `target` равно `webview`, то ссылку надо открывать в
      webview, а не в браузере.
* `priority` - число - приоритет баннера. Чем выше, тем более приоритетным считается баннер.
* `start_date` - дата начала действия баннера (таймстемп в UTC). Бекенд может начать возвращать баннер до того,
    как его фактически потребуется показать, чтобы клиент мог закешировать ответ. При этом бекенд может изменить
    параметры такого заранее выданного баннера, например, текст или URL изображения. При демонстрации баннера с данным
    `id` всегда должен использоваться самый свежий набор параметров, полученный с бекенда (с учетом механизмов
    кеширования на стороне клиента).
* `end_date` - дата окончания действия баннера (таймстемп в UTC).
* `screen` - строка-идентификатор экрана показа баннера (значение непрозрачно для бекенда).
* `origin` - источник баннера. `yandex-taxi` или некий идентификатор партнера

### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "supported_promotions": ["Tesla", "Bentley"],
    }

-

    {
        "active_promotions": [{
            "name": "Tesla",
            "cities": ["Москва", "Санкт-Петербург"],
            "image_tags": ["tesla_1", "tesla_2"],
        }],
    }

### Пример 2 (полноэкранный баннер)

    {
        "id": "1234567890abcdefghijkl0987654321",
        "supported_promotions": ["Tesla", "Bentley"],
        "fullscreen_banner": {
            "size_hint": 230,
            "banners_seen": ["banner_30062015"]
        }
    }

-

    {
        "active_promotions": [{
            "name": "Tesla",
            "cities": ["Москва", "Санкт-Петербург"],
            "image_tags": ["tesla"],
        }],
        "fullscreen_banner": [{
            "id": "banner_30062015",
            "cities": ["Москва", "Санкт-Петербург", "Екатеринбург"],
            "caption": "Новое Я.Такси!",
            "text": "Попробуйте наши новые вкусные фичи. Вам без них плохо.",
            "image": {
                "url": "http://somewhere.in.yandex.net/static/images/banner1.png",
                "size_hint": 240
            },
            "background": {
                "url": "http://somewhere.in.yandex.net/static/images/banner1_bg.png",
                "size_hint": 240
            },
            "logo": {
                "url": "http://somewhere.in.yandex.net/static/images/banner1_logo.png",
                "size_hint": 240
            },
            "origin": "yandex-taxi",
            "priority": 1,
            "widgets": {
                "close_button": true,
                "menu_button": true,
                "action_button": {
                    "label": "Я все понял",
                    "deeplink": "some/link"
                }
            },
            "start_date": "2015-07-03T00:00:00+0000",
            "end_date": "2015-07-31T00:00:00+0000",
            "screen": "summary"
        }]
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __supported_promotions__ `t: array`     список идентификаторов поддерживаемых промо-акций
*    __fullscreen_banner__ `t: object`     ?
    *   ⋮ __banners_seen__ `t: array`     список id баннеров, уже просмотренных клиентом
    *   ⋮ __size_hint__ `t: integer`     число, обозначающее желаемый размер (смысл значения зависит от клиента)

### Допустимые параметры ответа

*   ⋮ __active_promotions__ `t: promotion_list`     ?
    *   ⋮ __response__ `t: promotion_list`     объект ответа целиком
*    __fullscreen_banners__ `t: array`     ?
    *   ⋮ __response__ `t: fullscreen_banner`     объект ответа целиком

<a name="request_pushack"></a>
## pushack
### Описание

Уведомление backend'а о том, что пуш доставлен на клиент.
Ручку дергают клиенты (Android, iOS), когда наше приложение получает пуш.
Клиенты подтверждают получение любого пуша, для которого в payload был передан id пуша.
Сейчас id пуша передается для системных пушей (db.notify_queue), а также для маркетинговых пушей,
рассылаемых крон-скриптом notify_users_yt по таблице YT.


Различение источника пушей делается по префиксу push_id.
Такое решение принято для сохранения обратной совместимости со старыми клиентами.
Системные пуши: префикса нет
Маркетинговые пуши по YT: префикс = "yt_table"
и так далее

### Пример

    {
        "id": "562eab0df9744b7e919f40340d2d7652",
        "push_id": "yt_table:795c1f10513a46e7a75a5c7a39e21c2d"
    }

-

    {
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __push_id__ `t: string`     идентификатор пуша

### Допустимые параметры ответа


<a name="request_reorder"></a>
## reorder
### Описание

Изменение параметров заказа.

Для срочных заказов, находящихся в статусе `search` (машина еще не найдена), возможно изменение
некоторых параметров заказа. Как правило, это делается для тех заказов, на которые никто не
откликается в течение долгого времени (например, для тех, по которым сервер предложил параметр
`calibrate` в ответе на запрос `taxisearch`).

Возможно изменение одного или нескольких параметров из:

*  `class`
*  `service_level`
*  `requirements`
*  `due`
*  `parks`

Изменение параметров заказа происходит путем отмены исходного заказа и создания вместо него нового.
При этом в новом заказе будут изменены те параметры, которые приложение передаст в запросе.
Обратите внимание, что параметры заменяются целиком - например, если в исходном заказе было
требование `universal`, а в запросе передано требование `conditioner`, то в новом заказе будет
только требование `conditioner`, а не оба требования вместе.

Если на исходный заказ уже найден исполнитель, то отменять его нецелесообразно, поэтому для таких
случаев предусмотрен особый параметр `found`. В противном случае будет возвращен новый
идентификатор заказа, которым следует пользоваться во всех последующих запросах обычным способом.

Требование `coupon` нельзя добавить или убрать запросом `reorder`.

### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1234567890mnopqrstuvwx0987654321",
        "class": [
            "econom",
            "business"
        ],
        "requirements": {
            "animaltransport": true,
        },
        "due": "2013-04-01T14:00:00+0400"
    }

-

    {
        "orderid": "1234567890yzabcdefghij0987654321",
        "status": "search"
    }

### Допустимые параметры запроса

*   ⋮ __decision_id__ `t: uuid4`     идентификатор выбранного пользователем решения
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __orderid__ `t: uuid4`     идентификатор исходного заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа

*  Вариант 1
    *   ⋮ __found__ `t: boolean`     найдена машина на исходный заказ, перезаказа не будет
*  Вариант 2
    *   ⋮ __orderid__ `t: uuid4`     идентификатор созданного заказа
        *   ⋮ __response__ `t: uuid4`     объект ответа целиком
    *   ⋮ __status__ `t: order_status`     статус созданного заказа
        *   ⋮ __response__ `t: order_status`     объект ответа целиком
    *    __coupon__ `t: coupon_info`     предъявленный к оплате купон
        *   ⋮ __response__ `t: coupon_info`     объект ответа целиком

<a name="request_routestats"></a>
## routestats
### Описание

Статистика по маршруту и информация о категориях обслуживания.

Если клиент передаёт начальную и конечную точку маршрута, сервер
возвращает информация по протяжённости и продолжительности поездки,
`distance` и `time` соответственно. Параметр `jams` сообщает клиенту,
как был построен маршрут: с учётом или без учёта пробок. Параметр `center_tab`
сообщает клиенту, что нужно центрировать табы.

Если передан город, возвращается информация о категориях обслуживания
`service_levels`. Перед заказом клиент должен выбрать одну из категорий,
и передать в заказ значение `service_level`.

Если переданы начальная и конечная точка маршрута, город, а также время
подачи машины `due`, список исключённых таксопарков `parks` и требования
к автомобилю `requirements`, сервер расчитает и вернёт *примерную*
стоимость поездки по всем тарифам всех таксопарков `calc`, а в объекты
списка `service_levels` может быть добавлено поле `price` - при наличии
таксопарков, удовлетворяющих конкретному уровню `service_level`.
При наличии возможности сервер также обогатит объекты `service_level`
информацией об ожидаемом времени подачи машины с данным уровнем
обслуживания - поле `estimated_waiting`, а также информацией о минимальном
тарифе (см. примеры). Если в данный момент заказ по данному тарифу сделать
невозможно, будет передан объект `tariff_unavailable`, содержащий поля
`code` и `message` (код ошибки и ее текст).

В случае, если в требованиях в запросе (`requirements`) был передан код
купона (`coupon`), цена `price` будет указана с учетом купона.
Немодифицированная цена при этом возвращается в `price_ride`. Кроме того,
в ответе сервера будет присутствовать объект `coupon`, имеющий структуру,
аналогичную возвращаемой на запрос `order`.

В случае, если карта выбрана способом оплаты для данного заказа, клиент должен
передавать идентификатор карты в объекте `payment`, имеющем ту же структуру,
что и в ручке `order`. Аналогично с корпоративной поездкой.

Если в запросе передается код купона, необходимо, чтобы пользователь был
авторизован. Иначе будет возвращен код 401.

Если переданы параметры `due` и `city` и не передан маршрут, сервер
возвращает минимальную стоимость поездки по городу.

Если переданы параметры `due` и `city` и передана только одна точка
маршрута, сервер возвращает минимальную стоимость поездки с учётом
стоимости подачи машины до заданной точки маршрута.

Если в запросе будет передан параметр `supports_forced_surge = true`, и в этой
зоне включён принудительный сурж, то в `service_level` может придти поле
`forced_surge`, в котором хранится информация о текущем сурже, и часть сумм
будет пересчитана, кроме `details_tariff.price` и `details_tariff.icon`.

### Оптимизация ожидаемого времени подачи

Вычисление ожидаемого времени подачи на сервере - трудоемкая операция. Поэтому клиент
должен избегать запрашивать его без лишней необходимости.

Для управления этим процессом предусмотрены два булевых флага:
- В запросе: `skip_estimated_waiting`. Если `true`, сервер не вычисляет и не возвращает
ожидаемое время подачи. В качестве побочного эффекта пропадает возможность определить
недоступность тарифа.
- В ответе: `cache_estimated_waiting`, объект с двумя целочисленными полями: `distance` и
`ttl`. Если присутствует, клиент не должен перезапрашивать ожидаемое время подачи при смещении
пина ближе, чем на `distance` метров. `ttl` задает время жизни данных в кэше. Если `distance`
равен 0, кэш на клиенте не используется. Если `ttl` равен 0, кэш на клиенте не используется.

Сейчас эта функциональность отключена (CACHE_EST_WAITING_ENABLE=false) и в
ответе `cache_estimated_waiting` не передаётся. С браузера запросы всё равно
идут с параметром `skip_estimated_waiting=true` потому что в браузере время
прибытия такси не отображется.

### Изменения в протокле для нового саммари
Для поддержки нового саммари в ручке /routestats сделали следующие изменения:
1.  Клиент передаёт новый параметр ```{... "summary_version": 2, ...}``` в теле
запроса
2.  Для того чтобы клиент мог отобразить цену без скидки на новом саммари
добавляем новое поле в ответе service_levels.original_price
3.  Для того чтобы на кнопке вызова такси пропал текст про цену и времени
поездки, в ответе не будет title и title_markup если summary_version==2.
4.  Клиент должен брать цену поездки из поля
service_levels.description_parts.value. Сейчас когда точка Б указана, текст
получется то что надо. Когда точки Б нет или построить маршрут не удалось текст
выходит ```99 $SIGN$CURRENCY$ за первые 5 мин и 2 км```
а для нового саммари надо чтобы было ```от 99 $SIGN$CURRENCY$```.
Это разруливается на бекенде проверкой флага summary_version==2.
5.  Если "selected_class_only": false и "suggest_alternatives": true возвращаем
**цены по всем классам**, а **альтпины только для выбранного**.
Сейчас при запросе с альтпинами цены возвращаются всегда только для выбранного
как и сами альтернативы.
6.  Добавляем новый параметр в запрос ```estimate_waiting_selected_only```.
Нужно для того чтобы бекенд понимал что нужно расчитывать время для всех классов
(сменили точку подачи) или только для выбранного (потрогали крутяшку).
7.  Минимальная сумма поездки по тарифу в поле
service_levels.description_parts.value будет зависеть от суржа, скидки и купонов
(для старого саммари не зависит). Это поведение регулируется конфигом
8.  Цена по всем тарифам должна быть с учётом пожеланий. Если класс не
поддерживает выбранные пожелания (например лыжи), то стоимость не отображается
9.  Если у категории в тарифе выставлен флаг "запрашивать точку Б" в ответе
routestats должно быть ```"requirements": {"destination": true}```
(нужно для пула)

### Запрос с главного экрана
```
{
  "extended_description": true, 
  "format_currency": true, 
  "id": "2f641d32c21744a2821bc6184cc65cf1", 
  "payment": {
    "payment_method_id": "card-x6936", 
    "type": "card"
  }, 
  "position_accuracy": 0, 
  "route": [
    [
      37.650292258752216, 
      55.8093720753486
    ]
  ], 
  "skip_estimated_waiting": false, 
  "supported_markup": "tml-0.1", 
  "supports_forced_surge": true, 
  "supports_hideable_tariffs": true, 
  "supports_no_cars_available": true, 
  "surge_fake_pin": false, 
  "with_title": true, 
  "zone_name": "moscow"
}
```

```
{
  "calc": [], 
  "center_tab": true, 
  "currency_rules": {
    "code": "RUB", 
    "sign": "₽", 
    "template": "$VALUE$ $SIGN$$CURRENCY$", 
    "text": "руб."
  }, 
  "notify": null, 
  "service_levels": [
    {
      "cars": [
        "Hyundai Solaris", 
        "Kia Rio", 
        "Ford Focus", 
        "Renault Fluence"
      ], 
      "class": "econom", 
      "description": "99 $SIGN$$CURRENCY$ за первые 4 мин и 2 км", 
      "description_parts": {
        "prefix": "", 
        "suffix": "", 
        "value": "99 $SIGN$$CURRENCY$ за первые 4 мин и 2 км"
      }, 
      "details": [
        {
          "description": "всего", 
          "price": "99 $SIGN$$CURRENCY$"
        }
      ], 
      "details_tariff": [
        {
          "type": "price", 
          "value": "от 99 $SIGN$$CURRENCY$"
        }, 
        {
          "type": "icon", 
          "value": "от 99 $SIGN$$CURRENCY$"
        }, 
        {
          "type": "comment", 
          "value": "включено 4 мин., далее 9 $SIGN$$CURRENCY$/мин."
        }, 
        {
          "type": "comment", 
          "value": "включено 2 км, далее 9 $SIGN$$CURRENCY$/км"
        }
      ], 
      "estimated_waiting": {
        "message": "2 мин", 
        "seconds": 120
      }, 
      "is_hidden": false, 
      "name": "Эконом", 
      "price": "99 $SIGN$$CURRENCY$", 
      "service_level": 50
    }, 
    {
      "cars": [
        "Skoda Octavia", 
        "Ford Galaxy", 
        "Hyundai i40"
      ], 
      "class": "business", 
      "description": "199 $SIGN$$CURRENCY$ за первые 4 мин и 2 км", 
      "description_parts": {
        "prefix": "", 
        "suffix": "", 
        "value": "199 $SIGN$$CURRENCY$ за первые 4 мин и 2 км"
      }, 
      "details": [
        {
          "description": "всего", 
          "price": "199 $SIGN$$CURRENCY$"
        }
      ], 
      "details_tariff": [
        {
          "type": "price", 
          "value": "от 199 $SIGN$$CURRENCY$"
        }, 
        {
          "type": "icon", 
          "value": "от 199 $SIGN$$CURRENCY$"
        }, 
        {
          "type": "comment", 
          "value": "включено 4 мин., далее 12 $SIGN$$CURRENCY$/мин."
        }, 
        {
          "type": "comment", 
          "value": "включено 2 км, далее 12 $SIGN$$CURRENCY$/км"
        }
      ], 
      "estimated_waiting": {
        "message": "3 мин", 
        "seconds": 180
      }, 
      "is_hidden": false, 
      "name": "Комфорт", 
      "price": "199 $SIGN$$CURRENCY$", 
      "service_level": 70
    }, 
    {
      "cars": [
        "Nissan Teana", 
        "Toyota Camry", 
        "Lexus ES"
      ], 
      "class": "comfortplus", 
      "description": "199 $SIGN$$CURRENCY$ за первые 4 мин и 0 км", 
      "description_parts": {
        "prefix": "", 
        "suffix": "", 
        "value": "199 $SIGN$$CURRENCY$ за первые 4 мин и 0 км"
      }, 
      "details": [
        {
          "description": "всего", 
          "price": "199 $SIGN$$CURRENCY$"
        }
      ], 
      "details_tariff": [
        {
          "type": "price", 
          "value": "от 199 $SIGN$$CURRENCY$"
        }, 
        {
          "type": "icon", 
          "value": "от 199 $SIGN$$CURRENCY$"
        }, 
        {
          "type": "comment", 
          "value": "включено 4 мин., далее 13 $SIGN$$CURRENCY$/мин."
        }, 
        {
          "type": "comment", 
          "value": "включено 0 км, далее 13 $SIGN$$CURRENCY$/км"
        }
      ], 
      "estimated_waiting": {
        "message": "3 мин", 
        "seconds": 180
      }, 
      "is_hidden": false, 
      "name": "Комфорт+", 
      "price": "199 $SIGN$$CURRENCY$", 
      "service_level": 80
    }, 
    {
      "cars": [
        "Mercedes-Benz E-Class", 
        "Hyundai Equus"
      ], 
      "class": "vip", 
      "description": "299 $SIGN$$CURRENCY$ за первые 4 мин и 0 км", 
      "description_parts": {
        "prefix": "", 
        "suffix": "", 
        "value": "299 $SIGN$$CURRENCY$ за первые 4 мин и 0 км"
      }, 
      "details": [
        {
          "description": "всего", 
          "price": "299 $SIGN$$CURRENCY$"
        }
      ], 
      "details_tariff": [
        {
          "type": "price", 
          "value": "от 299 $SIGN$$CURRENCY$"
        }, 
        {
          "type": "icon", 
          "value": "от 299 $SIGN$$CURRENCY$"
        }, 
        {
          "type": "comment", 
          "value": "включено 4 мин., далее 18 $SIGN$$CURRENCY$/мин."
        }, 
        {
          "type": "comment", 
          "value": "включено 0 км, далее 18 $SIGN$$CURRENCY$/км"
        }
      ], 
      "estimated_waiting": {
        "message": "8 мин", 
        "seconds": 480
      }, 
      "is_hidden": false, 
      "name": "Бизнес", 
      "price": "299 $SIGN$$CURRENCY$", 
      "service_level": 90
    }, 
    {
      "cars": [
        "Ford Galaxy", 
        "Volkswagen Caddy"
      ], 
      "class": "minivan", 
      "description": "299 $SIGN$$CURRENCY$ за первые 4 мин и 0 км", 
      "description_parts": {
        "prefix": "", 
        "suffix": "", 
        "value": "299 $SIGN$$CURRENCY$ за первые 4 мин и 0 км"
      }, 
      "details": [
        {
          "description": "всего", 
          "price": "299 $SIGN$$CURRENCY$"
        }
      ], 
      "details_tariff": [
        {
          "type": "price", 
          "value": "от 199 $SIGN$$CURRENCY$"
        }, 
        {
          "type": "icon", 
          "value": "от 199 $SIGN$$CURRENCY$"
        }, 
        {
          "type": "comment", 
          "value": "включено 4 мин., далее 12 $SIGN$$CURRENCY$/мин."
        }, 
        {
          "type": "comment", 
          "value": "включено 0 км, далее 12 $SIGN$$CURRENCY$/км"
        }
      ], 
      "estimated_waiting": {
        "message": "11 мин", 
        "seconds": 660
      }, 
      "forced_surge": {
        "color_button": false, 
        "comment": "Вы сможете заказать такси по обычному тарифу, когда спрос уменьшится", 
        "description": "Тариф временно увеличен", 
        "display_card_icon": true, 
        "high_demand": true, 
        "order_comment": "Действует коэффициент ×1,5", 
        "reason": "Это вынужденная мера, так как спрос на такси чрезвычайно высок. Она позволит привлечь больше водителей.", 
        "show_popup": false, 
        "title": "×1,5", 
        "title_card": "× 1,5", 
        "value": 1.5
      }, 
      "is_hidden": false, 
      "name": "Минивэн", 
      "price": "299 $SIGN$$CURRENCY$", 
      "requirements": {
        "destination": true
      }, 
      "service_level": 95
    }
  ]
}
```

### Пример запроса с саммари

```
{
  "extended_description": true, 
  "format_currency": true, 
  "id": "dda99421638a410c9e5fe350da94b018", 
  "payment": {
    "payment_method_id": "corp-9b051f19a1a64b59ae00dc03eb67bc0d", 
    "type": "corp"
  }, 
  "position_accuracy": 0, 
  "route": [
    [
      37.61135202098592, 
      55.75355990214316
    ], 
    [
      37.584251403808594, 
      55.737545013427734
    ]
  ], 
  "selected_class": "business", 
  "selected_class_only": true, 
  "skip_estimated_waiting": true, 
  "suggest_alternatives": true, 
  "supported_markup": "tml-0.1", 
  "supports_forced_surge": true, 
  "supports_hideable_tariffs": true, 
  "supports_no_cars_available": true, 
  "surge_fake_pin": false, 
  "with_title": true, 
  "zone_name": "moscow"
}
```

```
{
  "alternatives": {
    "options": [
      {
        "address": {
          "city": "Москва", 
          "country": "Россия", 
          "description": "Москва, Россия", 
          "exact": false, 
          "full_text": "Россия, Москва, Большая Никитская улица", 
          "house": "", 
          "object_type": "другое", 
          "oid": "8061654", 
          "point": [
            37.61047963, 
            55.75509147
          ], 
          "short_text": "Большая Никитская улица", 
          "street": "Большая Никитская улица", 
          "type": "address"
        }, 
        "bubble_flag": "money", 
        "bubble_text": "Отсюда дешевле на 8 $SIGN$$CURRENCY$", 
        "description": "Поездка дешевле (+3 мин пешком)", 
        "offer": "f714820687394df5994af83bd5a023a2", 
        "service_levels": [
          {
            "cars": [
              "Skoda Octavia", 
              "Ford Galaxy", 
              "Hyundai i40"
            ], 
            "class": "business", 
            "description": "Поездка 382 $SIGN$$CURRENCY$, ~18 мин", 
            "description_parts": {
              "prefix": "", 
              "suffix": "", 
              "value": "382 $SIGN$$CURRENCY$"
            }, 
            "details": [
              {
                "description": "всего", 
                "price": "382 $SIGN$$CURRENCY$"
              }
            ], 
            "details_tariff": [
              {
                "type": "price", 
                "value": "от 199 $SIGN$$CURRENCY$"
              }, 
              {
                "type": "icon", 
                "value": "от 199 $SIGN$$CURRENCY$"
              }, 
              {
                "type": "comment", 
                "value": "включено 5 мин., далее 12 $SIGN$$CURRENCY$/мин."
              }, 
              {
                "type": "comment", 
                "value": "включено 2 км, далее 12 $SIGN$$CURRENCY$/км"
              }
            ], 
            "estimated_waiting": {
              "message": "20 мин", 
              "seconds": 1200
            }, 
            "is_hidden": false, 
            "name": "Комфорт", 
            "price": "380 $SIGN$$CURRENCY$", 
            "service_level": 70
          }
        ], 
        "walk": {
          "route": [
            [
              37.61142215, 
              55.75354882
            ], 
            [
              37.61159946, 
              55.75390414
            ], 
            [
              37.61159946, 
              55.75390414
            ], 
            [
              37.61180261, 
              55.75433419
            ], 
            [
              37.61180261, 
              55.75433419
            ], 
            [
              37.61181394, 
              55.75435795
            ], 
            [
              37.61181394, 
              55.75435795
            ], 
            [
              37.61183936, 
              55.75441637
            ], 
            [
              37.61183936, 
              55.75441637
            ], 
            [
              37.61185484, 
              55.75445293
            ], 
            [
              37.61187568, 
              55.75446604
            ], 
            [
              37.61190116, 
              55.75447672
            ], 
            [
              37.61191708, 
              55.7544892
            ], 
            [
              37.61192966, 
              55.75450319
            ], 
            [
              37.6119372, 
              55.75451756
            ], 
            [
              37.61194005, 
              55.75453344
            ], 
            [
              37.61193871, 
              55.75454838
            ], 
            [
              37.61193133, 
              55.75456417
            ], 
            [
              37.61191591, 
              55.75457882
            ], 
            [
              37.61187665, 
              55.75460348
            ], 
            [
              37.61184141, 
              55.75461832
            ], 
            [
              37.61184141, 
              55.75461832
            ], 
            [
              37.61188502, 
              55.75466522
            ], 
            [
              37.61188502, 
              55.75466522
            ], 
            [
              37.61193394, 
              55.75471891
            ], 
            [
              37.61193394, 
              55.75471891
            ], 
            [
              37.61054539, 
              55.75515638
            ], 
            [
              37.61054539, 
              55.75515638
            ], 
            [
              37.61047963, 
              55.75509147
            ]
          ]
        }
      }
    ], 
    "original_description": "Ближайшая точка подачи"
  }, 
  "cache_estimated_waiting": {
    "distance": 100, 
    "ttl": 20
  }, 
  "calc": [], 
  "center_tab": false, 
  "currency_rules": {
    "code": "RUB", 
    "sign": "₽", 
    "template": "$VALUE$ $SIGN$$CURRENCY$", 
    "text": "руб."
  }, 
  "distance": "4,5 км", 
  "is_fixed_price": true, 
  "jams": true, 
  "notify": null, 
  "offer": "8f32967a5c7242c78766b38c038028d2", 
  "service_levels": [
    {
      "cars": [
        "Skoda Octavia", 
        "Ford Galaxy", 
        "Hyundai i40"
      ], 
      "class": "business", 
      "description": "Поездка 390 $SIGN$$CURRENCY$, ~19 мин", 
      "description_parts": {
        "prefix": "", 
        "suffix": "", 
        "value": "390 $SIGN$$CURRENCY$"
      }, 
      "details": [
        {
          "description": "всего", 
          "price": "390 $SIGN$$CURRENCY$"
        }
      ], 
      "details_tariff": [
        {
          "type": "price", 
          "value": "от 199 $SIGN$$CURRENCY$"
        }, 
        {
          "type": "icon", 
          "value": "от 199 $SIGN$$CURRENCY$"
        }, 
        {
          "type": "comment", 
          "value": "включено 5 мин., далее 12 $SIGN$$CURRENCY$/мин."
        }, 
        {
          "type": "comment", 
          "value": "включено 2 км, далее 12 $SIGN$$CURRENCY$/км"
        }
      ], 
      "estimated_waiting": {
        "message": "11 мин", 
        "seconds": 660
      }, 
      "is_hidden": false, 
      "name": "Комфорт", 
      "price": "390 $SIGN$$CURRENCY$", 
      "service_level": 70
    }
  ], 
  "time": "19 мин"
}
```

### Допустимые параметры запроса

*    __alternative_suggested__ `t: boolean`     альтернативные точки подачи были получены в предыдущем запросе
*    __city__ `t: city`     город, в котором работает калькулятор тарифов или предварительный расчёт стоимости
    *   ⋮ __response__ `t: city`     объект ответа целиком
*    __due__ `t: string`  `f: due_time`   время подачи
*    __estimate_waiting_selected_only__ `t: boolean`     рассчитывать время подачи только для выбранного класса
*    __extended_description__ `t: boolean`     включать цену и расстояние для описания маршрута
*    __format_currency__ `t: boolean`      если передан, то в ответе передаем валюты в определенном формате
*    __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __parks__ `t: excluded_parks`     исключённые таксопарки
    *   ⋮ __response__ `t: excluded_parks`     объект ответа целиком
*    __payment__ `t: payment`     данные для оплаты картой (только при requirements.creditcard=true)
    *   ⋮ __response__ `t: payment`     объект ответа целиком
*    __position_accuracy__ `t: integer`     точноcть определения местоположения в метрах
*    __requirements__ `t: requirements_request`     требования к автомобилю
    *   ⋮ __response__ `t: requirements_request`     объект ответа целиком
*    __route__ `t: array`     маршрут поездки
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __selected_class__ `t: tariff_class`     выбранный класс обслуживания
    *   ⋮ __response__ `t: tariff_class`     объект ответа целиком
*    __selected_class_only__ `t: boolean`     выдавать информацию только по выбранному классу
*    __skip_estimated_waiting__ `t: boolean`     флаг, предписывающий не вычислять ожидаемое время подачи
*    __suggest_alternatives__ `t: boolean`     предлагать альтернативные точки подачи
*    __summary_version__ `t: integer`     версия summary на клиенте
*    __supported_markup__ `t: string` `v: tml-0.1`    поддерживаемый клиентом язык разметки
*    __supports_forced_surge__ `t: boolean`     данные о поддержке клиентом ответа forced_surge
*    __supports_hideable_tariffs__ `t: boolean`     данные о поддержке клиентом флага is_hidden
*    __supports_no_cars_available__ `t: boolean`     данные о поддержке клиентом ответа no_cars_available
*    __surge_fake_pin__ `t: boolean`     исключает запрос из расчета pins/free
*    __with_title__ `t: boolean`     который означает, что клиент поддерживает разбиение текста кнопки на title и description
*    __zone_name__ `t: string`     

### Допустимые параметры ответа

*    __alternatives__ `t: object`     Альтернативные точки подачи
    *    __options__ `t: array`     Список варинтов
        *   ⋮ __address__ `t: address`     Новый адрес подачи
            *   ⋮ __response__ `t: address`     объект ответа целиком
        *   ⋮ __service_levels__ `t: routestats_service_levels`     ?
            *   ⋮ __response__ `t: routestats_service_levels`     объект ответа целиком
        *   ⋮ __walk__ `t: object`     ?
            *   ⋮ __route__ `t: array`     маршрут до новой точки
                *   ⋮ __response__ `t: point`     объект ответа целиком
            *    __desctiption__ `t: `     описание новой точки
        *    __bubble_flag__ `t: string` `v: eta/time/money`    Флаг типа баббла
        *    __bubble_text__ `t: string`     Тест баббла
        *    __description__ `t: string`     Подпись пина
        *    __offer__ `t: string`     идентификатор предложения
    *    __original_description__ `t: string`     Описание оригинальной точки
*    __cache_estimated_waiting__ `t: object`     настройки кеширования ожидаемого времени подачи на клиенте
    *   ⋮ __distance__ `t: integer`     минимальное расстояние, при сдвиге на которое нужно пересчитывать время подачи
    *   ⋮ __ttl__ `t: integer`     время жизни данных в кэше
*    __calc__ `t: array`     ориентировочная стоимость поездки по разным тарифам разных парков
    *   ⋮ __parkid__ `t: string`     идентификатор таксопарка
    *   ⋮ __tariffs__ `t: array`     примерные цены на поездку по тарифам
        *   ⋮ __id__ `t: string`     идентификатор тарифа
        *   ⋮ __price__ `t: string`     ориентировочная стоимость поездки
    *    __service_levels__ `t: array`     стоимость поездки с парком в зависимости от service_level
        *   ⋮ __price__ `t: string`     ориентировочная стоимость поездки (с учетом купона)
        *   ⋮ __service_level__ `t: service_level`     идентификатор положения (передаётся в order)
            *   ⋮ __response__ `t: service_level`     объект ответа целиком
*    __center_tab__ `t: boolean`     нужно ли центрировать выбранный таб
*    __coupon__ `t: coupon_info`     купон, который намеревается применить пользователь
    *   ⋮ __response__ `t: coupon_info`     объект ответа целиком
*    __currency_rules__ `t: currency_rules`     данные о валюте заказа (если клиент запросил)
    *   ⋮ __response__ `t: currency_rules`     объект ответа целиком
*    __distance__ `t: string`     расстояние по маршруту
*    __is_fixed_price__ `t: boolean`     предложение с фиксированной ценой
*    __jams__ `t: boolean`     оценка дана с учётом пробок
*    __offer__ `t: string`     идентификатор предложения
*    __service_levels__ `t: routestats_service_levels`     ?
    *   ⋮ __response__ `t: routestats_service_levels`     объект ответа целиком
*    __time__ `t: string`     время по маршруту

<a name="request_save_user_settings"></a>
## save_user_settings
https://st.yandex-team.ru/TAXIBACKEND-5620

У каждой настройки свой таимстемп. Клиент синхронизирует время с сервером и отвечает за генерацию таимстемпов. В ответе ручки launch передаётся хеш от всех настроек. Таким образом клиент понимает нужно ли обновлять настройки с сервера.

Если настройки сохранить не удалось клиент сохраняет настройки локально с таймстемпом. При загрузке настроек с сервера клиент сверяет таймстемпы локальных настроек с тем что он получил с бекенда.

На клиенте есть дефолтные значения всех настроек на случай если загрузить настройки с сервера не удаётся.

`id` - id пользователя

    /3.0/save-user-settings
    {
        "id": "00060bd51ffc4498aa8afbdcbb0d5ead",
        "settings": {
            "tips": {
                "value": 5,
                "timestamp": "2015-12-01T17:08:18+0300"
            }
        }
    }

Ответ:

Если настройки удалось сохранить

    200
    {
        "user_settings_hash": "abcdefg"
    }

Если пользователя не удалось найти

    404
    {}

Если пользователь неавторизован

    401
    {}

Если хотя бы у одной настройки таимстемп в запросе меньше чем на бекенде.

    409
    {}


**launch**

Добавилось новое поле `user_settings_hash`

    {
        ...
        "user_settings_hash": "abcdefg"
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __settings__ `t: object`     значения и таимстемпы настроек

### Допустимые параметры ответа

*    __user_settings_hash__ `t: string`     хеш от настроек

<a name="request_setdontcall"></a>
## setdontcall
### Описание

Метод `/setdontcall` позволяет изменить настройку "Не звонить".
Значение (true/false) передается в поле `"dont_call"`

### Заголовки
Сервер вернет заголовок Last-Orders-Modified
(в формате '2015-11-27T13:21:16.662842'). Как его использовать - см.
['/changes'](changes.md)

Клиент передает в поле `"created_time"` время (синхронизированное с
сервером) создания изменения.

В ответе в поле `"change_id"` сервер вернет уникальный идентификатор изменения.
По этому идентификатору клиент может следить за статусом изменения.
В поле "status" возвращается текущий статус изменения: "pending|failed|success".

Если сервер вернул 200, значит изменение было сохранено сервером, и волноваться
не нужно.

А вот если ...

### Коды ошибок

##### 404
Заказ с переданным *orderid* не был найден.

##### 406
Действие не может быть применено.

##### 409
Настройка уже была изменена клиентом с более поздним `"created_time"`.


### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1234567890mnopqrstuvwx0987654321",
        "created_time": "2013-03-13T08:57:22+0000",
        "dont_call": true
    }

-

    {
        "change_id": "7116f3e79bc843a09ef13756b04d19dc",
        "status": "success"
        "name": "dont_call",
        "value": true
    }

### Допустимые параметры запроса

*   ⋮ __created_time__ `t: string`  `f: date-time`   UTC-время создания изменения
*   ⋮ __dont_call__ `t: boolean`     новое значение настройки 'Не звонить'
*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __orderid__ `t: uuid4`     идентификатор заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __change_id__ `t: uuid4`     уникальный идентификатор изменения
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __name__ `t: string`     тип изменения
*   ⋮ __status__ `t: change_status`     статус изменения
    *   ⋮ __response__ `t: change_status`     объект ответа целиком
*   ⋮ __value__ `t: boolean`     значение изменения

<a name="request_setdontsms"></a>
## setdontsms
### Описание

Метод `/setdontsms` позволяет настроить, смсить ли пользвателю при изменении 
статуса такси.

Значение (true/false) передается в поле `"dont_sms"`

### Заголовки
Сервер вернет заголовок Last-Orders-Modified
(в формате '2015-11-27T13:21:16.662842'). Как его использовать - см.
['/changes'](changes.md)

Клиент передает в поле `"created_time"` время (синхронизированное с
сервером) создания изменения.

В ответе в поле `"change_id"` сервер вернет уникальный идентификатор изменения.
По этому идентификатору клиент может следить за статусом изменения.
В поле "status" возвращается текущий статус изменения: "pending|failed|success".

Если сервер вернул 200, значит изменение было сохранено сервером, и волноваться
не нужно.

А вот если ...

### Коды ошибок

##### 404
Заказ с переданным *orderid* не был найден.

##### 406
Действие не может быть применено.

##### 409
Настройка уже была изменена клиентом с более поздним `"created_time"`.


### Пример

{
"id": "1234567890abcdefghijkl0987654321",
"orderid": "1234567890mnopqrstuvwx0987654321",
"created_time": "2013-03-13T08:57:22+0000",
"dont_sms": true
}

-

{
"change_id": "7116f3e79bc843a09ef13756b04d19dc",
"status": "success"
"name": "dont_sms",
"value": true
}

### Допустимые параметры запроса

*   ⋮ __created_time__ `t: string`  `f: date-time`   UTC-время создания изменения
*   ⋮ __dont_sms__ `t: boolean`     новое значение настройки 'Не смсить'
*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __orderid__ `t: uuid4`     идентификатор заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __change_id__ `t: uuid4`     уникальный идентификатор изменения
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __name__ `t: string`     тип изменения
*   ⋮ __status__ `t: change_status`     статус изменения
    *   ⋮ __response__ `t: change_status`     объект ответа целиком
*   ⋮ __value__ `t: boolean`     значение изменения

<a name="request_sharedroute"></a>
## sharedroute
### Описание

Ручка отдает редко меняющуюуся информацию о маршруте, который пользователь желает расшарить.
Сюда входит статус заказа, сведения об исполнителе и т.п.

В данный момент является урезанной версией `3.0/taxiontheway`, однако, вынесена в самостоятельную
ручку для обеспечения возможности независимой эволюции.

Ручка не требует авторизации. В качестве идентификатора передается ключ для шаринга маршрута
(route sharing key).

### Пример

    {
        "id": "97d4418d5ecf41859da8825cf76059b1",
        "key": "PvJWAPcFqij61g1YcK5lBMPDFt-AEmsSMkL_w3Yhsgc="
    }

-

    {
        "status": "driving",
        "driver": {
            "color": "черный",
            "color_code": "FFFFFF",
            "model": "мерседес",
            "name": "Сергей",
            "plates": "А111АА97"
        },
        "request": {
            "route": [
                {
                    "country": "Россия",
                    "fullname": "Россия, Москва, Новосущевская, 1",
                    "geopoint": [
                        33.6,
                        55.1
                    ],
                    "locality": "Москва",
                    "porchnumber": "1",
                    "premisenumber": "1",
                    "thoroughfare": "Новосущевская"
                    "short_text": "Новосущевская, 1",
                    "short_text_from": "Новосущевская, 1",
                    "short_text_to": "Новосущевская, 1",
                },
                {
                    "country": "Россия",
                    "fullname": "Россия, Москва, 8 Марта, 4",
                    "geopoint": [
                        33.1,
                        52.1
                    ],
                    "locality": "Москва",
                    "porchnumber": "",
                    "premisenumber": "4",
                    "thoroughfare": "8 Марта"
                    "short_text": "8 Марта, 4",
                    "short_text_from": "8 Марта, 4",
                    "short_text_to": "8 Марта, 4",
                }
            ],
        },
        "routeinfo": {
            "distance_left": 5876.34,
            "time_left": 269.1744999999996
        },
    }

### Допустимые параметры запроса

*   ⋮ __key__ `t: string`     ключ маршрута

### Допустимые параметры ответа

*   ⋮ __status__ `t: order_status`     статус заказа
    *   ⋮ __response__ `t: order_status`     объект ответа целиком
*    __driver__ `t: object`     информация о водителе и автомобиле
    *    __color__ `t: string`     цвет машины
    *    __color_code__ `t: string`     код цвета машины
    *    __model__ `t: string`     модель машины
    *    __name__ `t: string`     имя водителя
    *    __plates__ `t: string`     госномер машины
*    __request__ `t: object`     информация о заказе
    *   ⋮ __route__ `t: array`     маршрут заказа
        *   ⋮ __response__ `t: route_point`     объект ответа целиком
*    __routeinfo__ `t: object`     текущая информация по маршруту
    *    __distance_left__ `t: number`     расстояние до точки назначения в метрах (по данным маршрутизатора)
    *    __time_left__ `t: number`     прогнозируемое время до конца поездки в секундах (по данным маршрутизатора)

<a name="request_sharedroutetrack"></a>
## sharedroutetrack
### Описание

Ручка отдает маршрут водителя, который пользователь пожелал расшарить.
Не требует авторизации.

Семантически полностью аналогична `taxiroute`, за исключением следующего:
    * Вместо `id` и `orderid` в ручку передается единственный параметр `key` -
        ключ расшаренного маршрута (route sharing key).
    * Параметры `driverid` и `key` являются взаимоисключающими.

### Пример 1

        {
                "key": "PvJWAPcFqij61g1YcK5lBMPDFt-AEmsSMkL_w3Yhsgc=",
                "timestamp": "2015-12-01T17:08:18+0300",
                "coordinates": [
                        37.58888,
                        55.734761
                ]
        }

-

        {
                "coordinates": [
                        37.59431,
                        55.74381
                ],
                "route": [{
                        "src": [37.58888, 55.734761],
                        "dst": [37.59431, 55.74381],
                        "distance": 1062.36420
                }],
                "start_timestamp": "2015-12-01T17:08:18+0300",
                "timestamp": "2015-12-01T17:48:18+0300"
        }

### Допустимые параметры запроса

*   ⋮ __key__ `t: string`     ключ маршрута
*    __coordinates__ `t: point`     откуда прокладывать маршрут
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __driverid__ `t: string`     идентификатор водителя (для тестинга)
*    __timestamp__ `t: string`  `f: date-time`   время последнего полученного трека

### Допустимые параметры ответа

*   ⋮ __coordinates__ `t: point`     координаты последнего трека водителя
    *   ⋮ __response__ `t: point`     объект ответа целиком
*   ⋮ __route__ `t: array`     маршрут от указанной точки до текущего положения водителя
    *   ⋮ __distance__ `t: number`     длина отрезка
    *   ⋮ __dst__ `t: point`     координаты конца отрезка
        *   ⋮ __response__ `t: point`     объект ответа целиком
    *   ⋮ __src__ `t: point`     координаты начала отрезка
        *   ⋮ __response__ `t: point`     объект ответа целиком
*   ⋮ __start_timestamp__ `t: string`  `f: date-time`   время первой точки на маршруте
*   ⋮ __timestamp__ `t: string`  `f: date-time`   время последнего трека водителя
*    __direction__ `t: number`     направление движения водителя

<a name="request_suggesteddestinations"></a>
## suggesteddestinations
### Описание

Список адресов, куда пользователь скорее всего поедет. Ручка принимает на вход id пользователя,
его текущие координаты и количество возвращаемых точек. Возвращает список адресов из истории пользователя.
Если адрес встречается несколько раз, используется только самый новый. Точки упорядочены по дате заказа по убыванию.
Не показываются слишком близкие точки и слишком далекие.
Если у пользователя нет истории, возвращаются хотспоты города, в который попадает переданная точка.

Необязательный параметр "with_userplaces" = true меняет поведение ручки:
В список адресов подмешиваются userplaces. Причем адреса возвращаются в обычном формате, а userplaces в том же формате,
что и в ручке userplaces.
Для различения адресов и userplaces ко всем объектам выдачи добавляется булево поле "is_userplace"
Клиент может определить, пытался ли backend добавлять в выдачу userplaces по флагу "with_userplaces" = true в ответе -
он добавляется только если клиент указал "with_userplaces" = true в запросе и при этом эксперимент был включен
Подробности в тикете TAXIBACKEND-8143

**Примечание:** поля `short_text_from` и `short_text_to` на данный момент возвращают именительный падеж.

### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "ll": [61.471157,57.014094],
        "results": 5
    }

-

    {
        "objects": [
            {
                "city": "Москва",
                "country": "Россия",
                "exact": true,
                "full_text": "Россия, Москва, Пресненская набережная, 12",
                "house": "12",
                "object_type": "другое",
                "point": [
                    37.536831999999997,
                    55.749586999999998
                ],
                "short_text": "Пресненская набережная, 12",
                "short_text_from": "Пресненская набережная, 12",
                "short_text_to": "Пресненская набережная, 12",
                "street": "Пресненская набережная",
                "type": "address",
                "description": "Москва, Россия"
            }
        ]
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __ll__ `t: point`     местонахождение пользователя
    *   ⋮ __response__ `t: point`     объект ответа целиком
*   ⋮ __results__ `t: integer`     ограничение на количество возвращаемых результатов

### Допустимые параметры ответа

*   ⋮ __objects__ `t: array`     список всех найденных адресов и/или организаций
    *   ⋮ __city__ `t: string`     город
    *   ⋮ __country__ `t: string`     страна
    *   ⋮ __exact__ `t: boolean`     точно ли определен адрес
    *   ⋮ __full_text__ `t: string`     полный адрес
    *   ⋮ __house__ `t: string`     дом
    *   ⋮ __object_type__ `t: string` `v: аэропорт/организация/другое`    классификация объекта или организации
    *   ⋮ __point__ `t: point`     координаты объекта или организации
        *   ⋮ __response__ `t: point`     объект ответа целиком
    *   ⋮ __short_text__ `t: string`     короткий адрес
    *   ⋮ __street__ `t: string`     улица
    *   ⋮ __type__ `t: string` `v: address/organization`    тип объекта - адрес или организация
    *    __description__ `t: string`     мелко-подробности
    *    __oid__ `t: string`     идентификатор объекта
    *    __short_text_from__ `t: string`     короткий адрес после предлога ОТ (откуда)
    *    __short_text_to__ `t: string`     короткий адрес после предлога ДО (куда)
    *    __tag__ `t: string`     тэг

<a name="request_suggestedpositions"></a>
## suggestedpositions
### Описание

Если пользователя не устроил найденный в nearestposition адрес, ему предлагается список предполагаемых адресов.
Ручка на вход получает id пользователя, координаты устройства и погрешность определения координат в метрах.
Возвращает список точек в указанном порядке:

1. адреса из истории пользователя, отранжированные по расстоянию до точки (не более 5 шт)
1. популярные адреса (не более 3 шт)
1. организации поблизости (не более 3 шт)

Все точки разные. Формат вывода совпадает с форматом geosearch.
Если прислан радиус неточности менее 100 метров, он будет увеличен до 100 метров.

Если в объекте будут переданы "comment" или "porchnumber", при выборе
объекта как места подачи данные параметры должны быть переданы в заказ.

**Примечание:** поля `short_text_from` и `short_text_to` на данный момент возвращают именительный падеж.

### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "ll": [61.471157,57.014094],
        "dx": 100
    }

-

    {
        "objects": [
            {
                "city": "Москва",
                "country": "Россия",
                "exact": true,
                "full_text": "Россия, Москва, Пресненская набережная, 12",
                "house": "12",
                "object_type": "другое",
                "point": [
                    37.536831999999997,
                    55.749586999999998
                ],
                "short_text": "Пресненская набережная, 12",
                "short_text_from": "Пресненская набережная, 12",
                "short_text_to": "Пресненская набережная, 12",
                "street": "Пресненская набережная",
                "type": "address",
                "description": "Москва, Россия",
                "comment": "остановитесь у дома",
                "porchnumber": "2"
            },
            {
                "city": "Москва",
                "country": "Россия",
                "exact": false,
                "full_text": "Россия, Москва, Пресненская набережная",
                "house": "",
                "object_type": "другое",
                "point": [
                    37.541556999999997,
                    55.746943000000002
                ],
                "short_text": "Пресненская набережная",
                "short_text_from": "Пресненская набережная, 12",
                "short_text_to": "Пресненская набережная, 12",
                "street": "Пресненская набережная",
                "type": "address",
                "description": "Москва, Россия"
            }
        ]
    }

### Допустимые параметры запроса

*   ⋮ __dx__ `t: integer`     погрешность определения координат в метрах
*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __ll__ `t: point`     местонахождение пользователя
    *   ⋮ __response__ `t: point`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __objects__ `t: array`     список всех найденных адресов и/или организаций
    *   ⋮ __city__ `t: string`     город
    *   ⋮ __country__ `t: string`     страна
    *   ⋮ __exact__ `t: boolean`     точно ли определен адрес
    *   ⋮ __full_text__ `t: string`     полный адрес
    *   ⋮ __house__ `t: string`     дом
    *   ⋮ __object_type__ `t: string` `v: аэропорт/организация/другое`    классификация объекта или организации
    *   ⋮ __point__ `t: point`     координаты объекта или организации
        *   ⋮ __response__ `t: point`     объект ответа целиком
    *   ⋮ __short_text__ `t: string`     короткий адрес
    *   ⋮ __street__ `t: string`     улица
    *   ⋮ __type__ `t: string` `v: address/organization`    тип объекта - адрес или организация
    *    __comment__ `t: string`     комментарий к заказу
    *    __description__ `t: string`     мелко-подробности
    *    __oid__ `t: string`     идентификатор объекта
    *    __porchnumber__ `t: string`     подъезд
    *    __short_text_from__ `t: string`     короткий адрес после предлога ОТ (откуда)
    *    __short_text_to__ `t: string`     короткий адрес после предлога ДО (куда)
    *    __tag__ `t: string`     тэг

<a name="request_tariffs"></a>
## tariffs
### Описание

Список тарифов, действующих в городе, заданном параметром `city`. Передача в ручку идентификатора сессии
пользователя (`id`) допускается, но не являются обязательной.

Мобильный клиент также должен передать желаемый размер (параметр `size_hint`) в виде некоторого числа.
Бекенд не пытается трактовать его значение. Клиенту будет возвращено изображение, значение
параметра для которого равно или превышает заданное; если таковое не будет найдено, будет возвращено
изображение с максимальным значением `size_hint`. Клиенты iOS и Android могут использовать собственную
независимую шкалу значений: так, одно конкретное изображение может соответствовать `size_hint` 2 в iOS
и 240 - в Android.

У каждого города с МРТ в `max_tariffs` у услуг и групп услуг добавлен параметр `id` такой, что
`service_name.<id>` будет совпадать с ключом строки в Танкере).

Возвращаемая структура данных, в основном, повторяет вывод `parkdetails` и старой ручки `cities` (до решения
TAXIBACKEND-2374). Однако, для каждого тарифа добавляются следующие поля:

  * `description` - описание тарифа
  * `image` - основное изображение (возвращается с учетом `size_hint`)
  * `icon` - изображение-пиктограмма
  * `service_levels` - список service_level'ов для данного тарифа. Используется для сопоставления
      с выводом routestats.

`image` и `icon` являются объектами следующей структуры:

    {
        "url": "ссылка, по которой доступен объект",
        "size_hint": "число, действительное значение size_hint (м.б. больше запрошенного)"
    }
    
Кроме того, если в параметрах ручки не передано `with_intervals: true`, из `max_tariffs` удаляются интервалы.

В случае, если у города нет МРТ, возвращается код ошибки 406 с пустым телом.

Если вы используете эту ручку, то, вероятно, в `3.0/cities` следует передавать флаг `exclude_tariffs: true`. 

### Пример

    {
        "city": "Екатеринбург",
        "size_hint": 300,
    }
    
-

    {
        "max_tariffs": [  like in parkdetails.tariffs  ]
    }


### Допустимые параметры запроса

*   ⋮ __city__ `t: city`     город
    *   ⋮ __response__ `t: city`     объект ответа целиком
*   ⋮ __size_hint__ `t: integer`     желаемый размер изображения (смысл зависит от клиента)
*    __format_currency__ `t: boolean`      если передан, то в ответе передаем валюты в определенном формате
*    __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __skin_version__ `t: integer`     номер версии скина
*    __supports_no_cars_available__ `t: boolean`     данные о поддержке клиентом ответа no_cars_available
*    __with_intervals__ `t: boolean`     включать ли в ответ ручки интервалы

### Допустимые параметры ответа

*    __currency_rules__ `t: currency_rules`     данные о валюте заказа (если клиент запросил)
    *   ⋮ __response__ `t: currency_rules`     объект ответа целиком
*    __max_tariffs__ `t: array`     список тарифов в городе
    *   ⋮ __description__ `t: string`     описание тарифа
    *   ⋮ __id__ `t: string`     идентификатор тарифа (уникален в пределах таксопарка)
    *   ⋮ __image__ `t: image`     изображение для тарифа
        *   ⋮ __response__ `t: image`     объект ответа целиком
    *   ⋮ __name__ `t: string`     название тарифа
    *    __can_be_default__ `t: boolean`     этот тариф может быть заполнен в качестве тарифа по умолчанию
    *    __class__ `t: tariff_class`     категория тарифа
        *   ⋮ __response__ `t: tariff_class`     объект ответа целиком
    *    __icon__ `t: image`     изображение для тарифа
        *   ⋮ __response__ `t: image`     объект ответа целиком
    *    __intervals__ `t: array`     временные интервалы
        *   ⋮ __id__ `t: string`     id интервала из МРТ
        *   ⋮ __name__ `t: string`     название интервала
        *   ⋮ __price_groups__ `t: array`     информация, разбитая по группам
            *   ⋮ __name__ `t: string`     название группы
            *   ⋮ __prices__ `t: array`     описание цен
                *   ⋮ __name__ `t: string`     наименование услуги
                *   ⋮ __price__ `t: string`     стоимость услуги
                *    __id__ `t: string`     id услуги
                *    __visual_group__ `t: string`     к какой логической группе относится этот ценник
            *    __comment__ `t: string`     комментарий
            *    __id__ `t: string`     id группы услуг
        *   ⋮ __schedule__ `t: schedule`     время действия интервала
            *   ⋮ __response__ `t: schedule`     объект ответа целиком
    *    __is_default__ `t: boolean`     этот тариф должен быть выбран как тариф по умолчанию (то есть если клиент в первый раз)
    *    __only_for_soon_orders__ `t: boolean`     по этому заказу можно делать только soon-заказы
    *    __restrict_by_payment_type__ `t: array`     поддерживаемые типы оплаты для данного тарифа (отсутствие поля означает поддержку всех типов)
        *   ⋮ __response__ `t: payment_method`     объект ответа целиком
    *    __service_levels__ `t: array`     значения service_levels, действительные для тарифа

<a name="request_tariffzonemap"></a>
## tariffzonemap
### Описание

Ручка для сайта. Отдает для выбранной пользователем зоны
список зон (название, полигон), которые будут упомянуты в описании тарифа.

### Пример запроса

    {
        "zone_name": "mytishchi",
        "lang": "ru"
    }
    
--

    {
        "areas": [
            {
                "geometry": {
                    "shell": [
                        [
                            37.285,
                            55.8058
                        ],
                        ...
                    ],
                    "holes": []
                },
                "name": "Москва"
            },
            {
                "geometry": {
                    "shell": [
                        [
                            37.738998,
                            55.934418
                        ],
                        ...
                    ],
                    "holes": []
                },
                "name": "Мытищи"
            },
            {
                "geometry": {
                    "shell": [
                        [
                            37.8508,
                            55.4261
                        ],
                        ...
                    ],
                    "holes": []
                },
                "name": "Аэропорт Домодедово"
            },
            {
                "geometry": {
                    "shell": [
                        [
                            37.3883,
                            55.9801
                        ],
                        ...
                    ],
                    "holes": []
                },
                "name": "Аэропорт Шереметьево"
            },
            {
                "geometry": {
                    "shell": [
                        [
                            37.2324,
                            55.5772
                        ],
                        ...
                    ],
                    "holes": []
                },
                "name": "Аэропорт Внуково"
            }
        ]
    }
    
    
Если зоны зона не найдена, возвращаем 404.

    {
        "zone_name": "myti",
        "lang": "ru"
    }
    
--

    HTTP/1.1 404 Not Found

### Допустимые параметры запроса

*   ⋮ __lang__ `t: string`     название языка для отображения названий зон
*   ⋮ __zone_name__ `t: home_zone_name`     название зоны
    *   ⋮ __response__ `t: home_zone_name`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __areas__ `t: array`     ?
    *   ⋮ __geometry__ `t: object`     информация о геометрии зоны
        *   ⋮ __holes__ `t: array`     ?
            *   ⋮ __response__ `t: polygon`     объект ответа целиком
        *   ⋮ __shell__ `t: polygon`     ?
            *   ⋮ __response__ `t: polygon`     объект ответа целиком
    *   ⋮ __name__ `t: string`     название зоны

<a name="request_taxicount"></a>
## taxicount
### Описание

Количество работающих в городе таксопарков, число автомобилей на линии.

Также сервер отдаёт информацию о лояльности пользователя и, если переданы параметры заказа (атрибуты `due`, `source`, `class`, `parks`, `airport`, `requirements`), даёт оценку необходимости калибровки (смягчения) параметров заказа.

### Важно

*   в параметре `parks` передаётся список **исключённых** пользователем таксопарков
*   информация о калибровке запрашивается каждый раз при изменении пользователем параметров заказа

### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "city": "Москва"
    }

-

    {
        "parks": 38,
        "online": 3211,
        "loyal": false
    }

### Пример оценки необходимости калибровки

    {
        "id": "1234567890abcdefghijkl0987654321",
        "city": "Москва",
        "source": [37.588404, 55.733931],
        "due": "2013-03-21T17:30:00+0400",
        "class": ["econom"],
        "parks": [],
        "airport": false,
        "requirements": {
            "nosmoking": true,
            "universal": true,
            "childchair": 3
        }
    }

-

    {
        "parks": 38,
        "online": 3211,
        "loyal": false,
        "calibrate": true
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __airport__ `t: boolean`     место подачи - аэропорт
*    __city__ `t: city`     город, в котором работает Яндекс.Такси
    *   ⋮ __response__ `t: city`     объект ответа целиком
*    __class__ `t: class`     классы автомобилей
    *   ⋮ __response__ `t: class`     объект ответа целиком
*    __due__ `t: string`  `f: due_time`   время подачи
*    __parks__ `t: excluded_parks`     исключённые таксопарки
    *   ⋮ __response__ `t: excluded_parks`     объект ответа целиком
*    __requirements__ `t: requirements_request`     требования к автомобилю
    *   ⋮ __response__ `t: requirements_request`     объект ответа целиком
*    __service_level__ `t: service_level`     классы автомобилей
    *   ⋮ __response__ `t: service_level`     объект ответа целиком
*    __source__ `t: point`     место подачи
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __zone_name__ `t: string`     название зоны

### Допустимые параметры ответа

*   ⋮ __loyal__ `t: boolean`     заказчик - лоялен
*   ⋮ __online__ `t: integer`     число водителей на линии
*   ⋮ __parks__ `t: integer`     число работающих таксопарков
*    __calibrate__ `t: boolean`     рекомендуем смягчить услвовия заказа

<a name="request_taxiontheway"></a>
## taxiontheway
### Описание

Экран выполнения заказа.

Рекомендуется повторять этот запрос через равные промежутки в течение всего выполнения заказа.
Параметр `status` укажет момент, когда выполнение заказа завершилось, и следует перейти на другой
экран.

Если пользователь при заказе ввел код купона, в поле `coupon` возвращается информация о валидности
и номинале купона.

Если известна стоимость поездки, в поле `cost_message` возвращается сообщение об этой стоимости.
Если поездка завершена или таксопарк заранее передал стоимость поездки, то в поле `cost` передается
стоимость поездки по расчетам таксопарка.

При использовании валидного купона в ответ добавляются поля `discount` (скидка в рублях) и
`final_cost` (сумма к оплате с учетом скидки по купону).

В поле `request` содержатся поля:
* `requirements` - все исходные требования заказа.
* `comment` - комментарий к заказу.

Если заказ оплачивается картой, но в какой-то момент выяснилось, что данная карта
не может использоваться для оплаты, в поле `request` добавляется поле `updated_requirements`
со следующей структурой (поле `requirements` при этом не изменяется):

    [
        {
            'requirement': 'creditcard',
            'value': false,
            'reason': {
                'code': 'UNUSABLE_CARD',
                'text': 'Некий текст для показа пользователю'
            }
        }
    ]

При `corp' типе оплате в `request` объекте может присутствовать поле `corp_cost_center`,
содержащий строку.

Возможные значения поля `code` (список кодов впоследствии может расширяться):

* `INVALID_CARD` - карта не может быть использована для оплаты
  (например, истёк срок действия карты)
* `UNUSABLE_CARD` - с карты не удалось списать средства
* `UNKNOWN_CARD` - данная карта не привязана к аккаунту пользователя
* `NEED_CVN` - для проведения платежа требуется ввод CVN
* `USER_CHANGE` - пользователь запросил смену способа оплаты

При изначальном способе оплаты "наличными" заказ может быть оплачен
картой (см. описание launch, paymentstatuses и payorder). В случае
успешной оплаты значение `updated_requirements` будет выглядеть
следующим образом:

    [
        {
            'requirement': 'creditcard',
            'value': true,
            'reason': {
                'code': 'INITIATED_BY_USER',
                'text': 'Некий текст для показа пользователю'
            }
        }
    ]

Сервер передаёт клиенту информацию об установленных им (клиентом) ранее
чаевых по заказу в поле `tips`. Поле `available` говорит о том, можно ли
для данного заказа устанавливать размер чаевых.

В случае автореордера клиенту необходимо отобразить текст, который
появляется в поле "autoreorder".

Сервер передаёт клиенту возможные причины "Что было не так?" в поле
"supported_feedback_choices". Формат поля такой же, как и в [/cities](cities.md),
 только вместо "cancelled_reason" - "low_rating_reason".

Для заказов в статусе "между" driving и finished (т.е. когда на заказе есть
перемещающийся автомобиль) в ответ сервера может добавляться строковое поле
`route_sharing_url`, содержащее URL для шаринга маршрута. Пользовательская
механика обработки этого поля описана в TAXIBACKEND-2846 и связанных задачах.

Клиент должен передавать серверу данные о своём местоположении в каждом
запросе (координаты и точность определения координат, см. `position`).

В случае, если отмена заказа запрещена, сервер передаёт клиенту поле
`cancel_disabled` со значением `true`. Отсутствие поля интерпретируется
как "отмена разрешена".

При отмене заказа пользователем или парком сервер возвращает информацию
об инициаторе отмены в поле `"cancelled_by"`.

Также сервер передаёт клиенту информацию об оставленном ранее отзыве в
поле `"feedback"`.

В поле `allowed_changes` сервер передает массив возможных действий
по изменению заказа.
Возможные элементы массива и их интерпретации:
* `{"name": "user_ready"}` - можно применять действие "Уже выхожу"
* `{"name": "porchnumber"}` - можно менять номер подъезда
* `{"name": "comment"}` - можно менять комментарий.
* `{"name": "destinations"}` - можно менять пункт назначения
* `{"name": "payment"}` - можно менять способ оплаты.
Если в массиве `allowed_changes` встречается действие с неизвестным
клиенту именем, то это действие надо игнорировать.
Поле "name" - обязательное поле в элементе массива. Элемент может
содержать любые другие произвольные поля.
Например, элемент с `{"name": "payment"}` может содержать поле
"available_methods" со списком возможных методов оплаты:
```json
{
    "name": "payment",
    "available_methods": ["card"]
}
```

Возможные значения в массиве "available_methods": `"card", "cash" и "corp"`.

В поле "pending_changes" сервер возвращает список текущих изменений в статусе
"pending".

Чтобы получать консистентные данные, клиент должен передавать header
Last-Orders-Modified. Как его использовать - ('/changes')[changes.md].

В поле `user_ready` передается информация о том, что пользователь нажал на
кнопку "Уже выхожу".

В поле `currency` передается код валюты заказа (RUB/AMD/BYR etc).

В поле `payment` передается информация о текущем способе оплаты заказа.
Например, для заказа за наличные:
```json
"payment": {
    "type": "cash"
}
```

Для заказа по карте:
```json
"payment": {
    "type": "card",
    "payment_method_id": "card-012345"
}
```

Для заказа по корпоративному счету:
```json
"payment": {
    "type": "corp",
    "payment_method_id": "corp-012345"
}
```

В поле `payment_changes` предаётся информация об изменениях в способе оплаты и причины этих изменений.
Это поле заменяет собой `update_requirements`.


**Примечание 1:** поля `short_text`, `short_text_from` и `short_text_to` возвращаются
только по заказам с новых клиентов (т.е. если в заказе было передано поле `short_text`).
**Примечание 2:** поля `short_text_from` и `short_text_to` на данный момент возвращают именительный падеж.

### Блок "cancel_rules"
```python
{
"cancel_rules": {
    "state": "string", # например, "free", "minimal", "paid"
    "state_change_estimate": 7500.42, # seconds, присылается, когда отмена бесплатна. Через сколько примерно врмени отмена станет платной,
    "title": "заголовок",  #если в зпросе был "show_text": true
    "message": "текст диалога о плтаной отмене, который нужно показывать, если отмена платная",  # если в зпросе был "show_text": true
    "message_support": "текст сообщения о том, что надо обратиться в суппорт",  # если в зпросе был "show_text": true
}
}
```

При отмене, клиент отправляет запрос с дополнительными полями
```python
{
"cancel_state": "string", # строка, присланная в предыдущем запросе totw. По умолчанию "free". Поле обязательное. (Если отсутствует - считаем старым клиентом)
"break": "user",
}
```

Если клиент хочет получить тексты диалога об отмене, он должен добавить в запрос
```python
{
"show_text": true, # показывать ли тексты сообщений об отмене. По умолчанию false
}
```

В ответ на запрос об отмене, бекенд может ответить стандартным ответом totw (все как раньше), 
**или** ответить с кодом `409 Conflict`
В послденем случае, в теле ответа содержится информация об ошибке в виде

```python
{
  "error": {
    "code": "ERROR_CANCEL_STATE_CHANGED", 
    "text": {
        "title": "описание",
        "message": "описание",
        "message_support": "описание"
    },
    "cancel_state": "new cancel state"
  }
}
```

В текущий момент код ошибки может быть `ERROR_CANCEL_STATE_CHANGED`, в том случае, 
если клиент передавал запрос с устаревшим cancel_state. 
В таком случае, `text` содержит диалог о платной отмене, 
который нужно показать пользователю 
(совпадает с полями `title`, `message`, `message_support` обычного ответа totw)

### Пример 1

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1234567890mnopqrstuvwx0987654321",
        "position": {
            "point": [37.504381, 55.730800],
            "dx": 1009
        }
    }

-

    {
        "driver": {
            "car": [37.64, 55.73],
            "color": "черный",
            "color_code": "FFFFFF",
            "model": "мерседес",
            "name": "Сергей",
            "overdue": false,
            "phone": "+71231231231",
            "plates": "А111АА97"
        },
        "loyal": false,
        "park": {
            "id": "000111src111",
            "name": "Аист",
            "phone": "+749533322111",
            "yamoney": true
        },
        "request": {
            "due": "2013-04-11T19:58:24+0400",
            "requirements": {
                "check": true
            },
            "comment": "some_comment",
            "route": [
                {
                    "country": "Россия",
                    "fullname": "Россия, Москва, Новосущевская, 1",
                    "geopoint": [
                        33.6,
                        55.1
                    ],
                    "locality": "Москва",
                    "porchnumber": "1",
                    "premisenumber": "1",
                    "thoroughfare": "Новосущевская"
                    "short_text": "Новосущевская, 1",
                    "short_text_from": "Новосущевская, 1",
                    "short_text_to": "Новосущевская, 1",
                },
                {
                    "country": "Россия",
                    "fullname": "Россия, Москва, 8 Марта, 4",
                    "geopoint": [
                        33.1,
                        52.1
                    ],
                    "locality": "Москва",
                    "porchnumber": "",
                    "premisenumber": "4",
                    "thoroughfare": "8 Марта"
                    "short_text": "8 Марта, 4",
                    "short_text_from": "8 Марта, 4",
                    "short_text_to": "8 Марта, 4",
                }
            ],
        },
        "status": "driving",
        "tariff": {
            "id": "1",
            "name": "эконом"
        },
        "coupon": {
            "valid": true,
            "value": 300
        },
        "cost_message": "Ориентировочная стоимость поездки 540 руб за 44 мин",
        "payment": {
            "type": "cash"
        },
        "payment_changes": [],
        "tips": {
            "type": "percent",
            "value": 0,
            "available": false
        },
        "autoreorder": {
            "text": "Найденный исполнитель не сможет приехать к Вам, мы ищем нового"
        },

        "feedback": {
            "msg": "Водитель курил и пил",
            "rating": 1,
            "choices": {
                "low_rating_reason": ["rudedriver"]
            },
            "call_me": true
        },
        "supported_feedback_choices": {
            "low_rating_reason": [
                {
                    "name": "driverlate",
                    "label": "Водитель опоздал"
                },
                {
                    "name": "rudedriver",
                    "label": "Грубый водитель"
                },
                {
                    "name": "smellycar",
                    "label": "Запах в машине"
                },
                {
                    "name": "carcondition",
                    "label": "Состояние автомобиля"
                },
                {
                    "name": "badroute",
                    "label": "Ездил кругами"
                },
                {
                    "name": "nochange",
                    "label": "Не было сдачи"
                }
            ],
            "allowed_changes": [
                {
                    "name": "porchnumber_and_comment"
                },
                {
                    "name": "payment",
                    "available_methods": ["card", "corp"]
                }
            ],
            "pending_changes": [
                {
                    "change_id": "7116f3e79bc843a09ef13756b04d19dc",
                    "name": "comment",
                    "value": "some comment",
                    "status": "pending"
                }
            ]
        },
        "cancel_disabled": true,
        "route_sharing_url": "https://taxi.yandex.ru/route-enter/PvJWAPcFqij61g1YcK5lBMPDFt-AEmsSMkL_w3Yhsgc=",
        "user_ready": true
    }

### Пример 2

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1234567890mnopqrstuvwx0987654321",
        "position": {
            "point": [37.504381, 55.730800],
            "dx": 1009
        }
    }

-

    {
        "driver": {
            "car": [37.64, 55.73],
            "color": "черный",
            "color_code": "FFFFFF",
            "model": "мерседес",
            "name": "Сергей",
            "overdue": false,
            "phone": "+71231231231",
            "plates": "А111АА97"
        },
        "loyal": false,
        "park": {
            "id": "000111src111",
            "name": "Аист",
            "phone": "+749533322111",
            "yamoney": true
        },
        "request": {
            "due": "2013-04-11T19:58:24+0400",
            "requirements": {
                "check": true,
                "corp": true
            },
            "comment": "some_comment",
            "corp_cost_center": "some_cost_center",
            "route": [
                {
                    "country": "Россия",
                    "fullname": "Россия, Москва, Новосущевская, 1",
                    "geopoint": [
                        33.6,
                        55.1
                    ],
                    "locality": "Москва",
                    "porchnumber": "1",
                    "premisenumber": "1",
                    "thoroughfare": "Новосущевская"
                    "short_text": "Новосущевская, 1",
                    "short_text_from": "Новосущевская, 1",
                    "short_text_to": "Новосущевская, 1",
                },
                {
                    "country": "Россия",
                    "fullname": "Россия, Москва, 8 Марта, 4",
                    "geopoint": [
                        33.1,
                        52.1
                    ],
                    "locality": "Москва",
                    "porchnumber": "",
                    "premisenumber": "4",
                    "thoroughfare": "8 Марта"
                    "short_text": "8 Марта, 4",
                    "short_text_from": "8 Марта, 4",
                    "short_text_to": "8 Марта, 4",
                }
            ],
        },
        "status": "complete",
        "tariff": {
            "id": "1",
            "name": "эконом"
        },
        "coupon": {
            "valid": true,
            "value": 300
        },
        "cost": 540,
        "discount": 300,
        "final_cost": 220,
        "cost_message": "Стоимость поездки 520 руб, к оплате 220 (скидка по купону 300 руб.)",
        "tips": {
            "type": "percent",
            "value": 0,
            "available": false
        },
        "feedback": {
            "msg": "Водитель курил и пил",
            "rating": 5
        },
        "supported_feedback_choices": {
            "low_rating_reason": [
                {
                    "name": "driverlate",
                    "label": "Водитель опоздал"
                },
                {
                    "name": "rudedriver",
                    "label": "Грубый водитель"
                },
                {
                    "name": "smellycar",
                    "label": "Запах в машине"
                },
                {
                    "name": "carcondition",
                    "label": "Состояние автомобиля"
                },
                {
                    "name": "badroute",
                    "label": "Ездил кругами"
                },
                {
                    "name": "nochange",
                    "label": "Не было сдачи"
                }
            ]
        },
        "cancel_disabled": false,
        "user_ready": true,
        "payment": {
            "type": "corp",
            "payment_method_id": "some_corp_id_from_method_payment_methods"
        },
        "payment_changes": []
    }


### Пример 3 (безналичный заказ, перешедший в наличный)

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1234567890mnopqrstuvwx0987654321",
        "position": {
            "point": [37.504381, 55.730800],
            "dx": 1009
        }
    }

-

    {
        "driver": {
            "car": [37.64, 55.73],
            "color_code": "FFFFFF",
            "color": "черный",
            "model": "мерседес",
            "name": "Сергей",
            "overdue": false,
            "phone": "+71231231231",
            "plates": "А111АА97"
        },
        "loyal": false,
        "park": {
            "id": "000111src111",
            "name": "Аист",
            "phone": "+749533322111",
            "yamoney": true
        },
        "request": {
            "due": "2013-04-11T19:58:24+0400",
            "requirements": {
                "creditcard": true,
                "check": true
            },
            "comment": "some_comment",
            "updated_requirements": [
                {
                    'requirement': 'creditcard',
                    'value': false,
                    'reason': {
                        'code': 'UNUSABLE_CARD',
                        'text': 'Заказ не может быть оплачен картой, готовьте наличные!'
                    }
                }
            ],
            "route": [
                {
                    "country": "Россия",
                    "fullname": "Россия, Москва, Новосущевская, 1",
                    "geopoint": [
                        33.6,
                        55.1
                    ],
                    "locality": "Москва",
                    "porchnumber": "1",
                    "premisenumber": "1",
                    "thoroughfare": "Новосущевская"
                    "short_text": "Новосущевская, 1",
                    "short_text_from": "Новосущевская, 1",
                    "short_text_to": "Новосущевская, 1",
                },
                {
                    "country": "Россия",
                    "fullname": "Россия, Москва, 8 Марта, 4",
                    "geopoint": [
                        33.1,
                        52.1
                    ],
                    "locality": "Москва",
                    "porchnumber": "",
                    "premisenumber": "4",
                    "thoroughfare": "8 Марта"
                    "short_text": "8 Марта, 4",
                    "short_text_from": "8 Марта, 4",
                    "short_text_to": "8 Марта, 4",
                }
            ],
        },
        "status": "driving",
        "tariff": {
            "id": "1",
            "name": "эконом"
        },
        "coupon": {
            "valid": true,
            "value": 300
        },
        "cost_message": "Ориентировочная стоимость поездки 540 руб за 44 мин",
        "payment": {
            "type": "card",
            "payment_method_id": "card-12345"
        },
        "payment_changes": [
            {
                "from": {
                    "type": "card",
                    "payment_method_id": "card-12345"
                },
                "to": {
                    "type": "cash",
                },
                "reason": {
                    "code": "UNUSABLE_CARD",
                    "text": "Заказ не может быть оплачен картой, готовьте наличные!"
                }
            }
        ],
        "tips": {
            "type": "percent",
            "value": 0,
            "available": false
        },
        "feedback": {
            "msg": "Водитель курил и пил",
            "call_me": false
        },
        "supported_feedback_choices": {
            "low_rating_reason": [
                {
                    "name": "driverlate",
                    "label": "Водитель опоздал"
                },
                {
                    "name": "rudedriver",
                    "label": "Грубый водитель"
                },
                {
                    "name": "smellycar",
                    "label": "Запах в машине"
                },
                {
                    "name": "carcondition",
                    "label": "Состояние автомобиля"
                },
                {
                    "name": "badroute",
                    "label": "Ездил кругами"
                },
                {
                    "name": "nochange",
                    "label": "Не было сдачи"
                }
            ]
        },
        "user_ready": true
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __orderid__ `t: uuid4`     идентификатор заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __break__ `t: string` `v: user/timeout`    отмена заказа
*    __format_currency__ `t: boolean`      если передан, то в ответе передаем валюты в определенном формате
*    __position__ `t: position`     ?
    *   ⋮ __response__ `t: position`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __cancel_disabled__ `t: boolean`     Отмена заказа запрещена
*   ⋮ __status__ `t: order_status`     статус заказа
    *   ⋮ __response__ `t: order_status`     объект ответа целиком
*    __allowed_changes__ `t: array`     возможные действия по изменению заказа
*    __autoreorder__ `t: object`     уведомление о поиске нового исполнителя
    *    __text__ `t: string`     текст сообщения, которое необходимо отобразить пользователю
*    __block_time__ `t: string`     время, на которое пользователь будет заблокирован
*    __busycars__ `t: array`     координаты занятых машин
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __cancelled_by__ `t: ` `v: park/user`    Инициатор отмены
*    __cost__ `t: number`     стоимость поездки (без учета купона)
*    __cost_as_str__ `t: string`     стоимость (без учета промокода) + валюта (с учетом format_currency)
*    __cost_message__ `t: string`     стоимость поездки текстом
*    __coupon__ `t: coupon_info`     предъявленный к оплате купон
    *   ⋮ __response__ `t: coupon_info`     объект ответа целиком
*    __currency_rules__ `t: currency_rules`     данные о валюте заказа (если клиент запросил)
    *   ⋮ __response__ `t: currency_rules`     объект ответа целиком
*    __discount__ `t: number`     скидка в рублях, если купон валидный
*    __dont_call__ `t: boolean`     значение ранее переданного флага dont_call
*    __dont_sms__ `t: boolean`     не смсить ли пользователю
*    __driver__ `t: object`     информация о водителе и автомобиле
    *    __car__ `t: point`     местоположение машины
        *   ⋮ __response__ `t: point`     объект ответа целиком
    *    __color__ `t: string`     цвет машины
    *    __color_code__ `t: string`     код цвета машины
    *    __forwarding__ `t: forwarding`     информация o переадресованном номере телефона водителя
        *   ⋮ __response__ `t: forwarding`     объект ответа целиком
    *    __model__ `t: string`     модель машины
    *    __name__ `t: string`     имя водителя
    *    __overdue__ `t: boolean`     трек слишком старый
    *    __phone__ `t: phone`     номер телефона водителя
        *   ⋮ __response__ `t: phone`     объект ответа целиком
    *    __plates__ `t: string`     госномер машины
    *    __way_time__ `t: integer`     время водителя в пути до места подачи (или -1, если оно слишком большое)
*    __feedback__ `t: user_feedback`     фидбэк пользователя на заказ
    *   ⋮ __response__ `t: user_feedback`     объект ответа целиком
*    __final_cost__ `t: number`     окончательная стоимость поездки с учетом купона
*    __final_cost_as_str__ `t: string`     стоимость (с учетом промокода) + валюта (с учетом format_currency)
*    __freecars__ `t: array`     координаты свободных машин
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __granted_promotions__ `t: array`     список идентификаторов промо-акций, которые были применены к заказу
*    __higher_class_dialog__ `t: object`     диалог о назначении машины из более высокого класса https://st.yandex-team.ru/TAXIBACKEND-2628
    *   ⋮ __tag__ `t: string`     имя тэга для получения изображения
    *   ⋮ __text__ `t: string`     текст диалога
    *   ⋮ __title__ `t: string`     заголовок диалога
*    __loyal__ `t: boolean`     лояльный пользователь
*    __park__ `t: object`     информация о таксопарке, исполняющем заказ
    *   ⋮ __id__ `t: string`     идентификатор таксопарка
    *   ⋮ __name__ `t: string`     название таксопарка
    *   ⋮ __phone__ `t: phone`     номер телефона диспетчерской (прямой или через шлюз переадресации)
        *   ⋮ __response__ `t: phone`     объект ответа целиком
    *   ⋮ __yamoney__ `t: boolean`     принимаются к оплате Яндекс.Деньги
    *    __forwarding__ `t: forwarding`     информация o переадресованном номере телефона диспетчерской
        *   ⋮ __response__ `t: forwarding`     объект ответа целиком
*    __payment__ `t: payment`     способ оплаты
    *   ⋮ __response__ `t: payment`     объект ответа целиком
*    __payment_changes__ `t: array`     смены метода оплаты
*    __pending_changes__ `t: array`     еще не примененные изменения по заказу
*    __reorder__ `t: reorder_suggestion`     предложение по обновлению требований к заказу
    *   ⋮ __response__ `t: reorder_suggestion`     объект ответа целиком
*    __request__ `t: object`     информация о заказе
    *   ⋮ __comment__ `t: string`     комментарий заказа
    *   ⋮ __due__ `t: string`  `f: date-time`   время подачи
    *   ⋮ __requirements__ `t: requirements_response`     исходные требования в заказе
        *   ⋮ __response__ `t: requirements_response`     объект ответа целиком
    *   ⋮ __route__ `t: array`     маршрут заказа
        *   ⋮ __response__ `t: route_point`     объект ответа целиком
    *    __corp_cost_center__ `t: string`     кост-центр поездки - только для корпоративных пользователей 
    *    __service_level__ `t: service_level`     положения селектора дёшево-комфортно
        *   ⋮ __response__ `t: service_level`     объект ответа целиком
    *    __surge_value__ `t: number`     значение суржпрайсинга для этого заказа
    *    __updated_requirements__ `t: updated_requirements`     требования, измененные в процессе заказа
        *   ⋮ __response__ `t: updated_requirements`     объект ответа целиком
*    __route_sharing_url__ `t: string`     URL для фичи шаринг маршрута
*    __routeinfo__ `t: object`     текущая информация по маршруту
    *    __distance_left__ `t: number`     расстояние до точки назначения в метрах (по данным маршрутизатора)
    *    __positions__ `t: array`     доп. точки по маршруту. Например, точка Б предыдущего заказа при цепочке заказов
        *    __info_key__ `t: string`     ключ описания точки
        *    __point__ `t: point`     точка на карте
            *   ⋮ __response__ `t: point`     объект ответа целиком
    *    __time_left__ `t: number`     ?
*    __source__ `t: point`     точка подачи машины
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __supported_feedback_choices__ `t: supported_feedback_choices`     возможные варианты фидбэка в этом городе
    *   ⋮ __response__ `t: supported_feedback_choices`     объект ответа целиком
*    __surge__ `t: surge`     информация для отображения диалога текущей ставки суржпрайсинга
    *   ⋮ __response__ `t: surge`     объект ответа целиком
*    __tariff__ `t: object`     информация о тарифе
    *   ⋮ __id__ `t: string`     идентификатор тарифа (уникален в пределах таксопарка)
    *   ⋮ __name__ `t: string`     название тарифа
*    __tips__ `t: user_tips`     чаевые, переданные пользователем на заказ (могут быть изменены в зависимости от состояния заказа)
    *   ⋮ __response__ `t: user_tips`     объект ответа целиком
*    __user_ready__ `t: boolean`     Пользователь на кнопку 'Уже выхожу'

<a name="request_taxiroute"></a>
## taxiroute
### Описание

Отдает маршрут поездки для анимации на стороне клиента. Требует авторизации.

Заказ, для которого нужно предоставить маршрут, задается либо параметром `orderid`.
Он должен принадлежать пользователю, аутентификационные данные которого переданы в
ручку.

В тестинге (или любом другом окружении, где включены спецкомментарии) допускается
передача параметра `driverid` (`clid_uuid`). В этом случае трек водителя берется
из прода (подразумевается г. Москва). `driverid` и `orderid` являются
взаимоисключающими.

Дополнительно, в теле запроса могут быть переданы параметры `timestamp` и `coordinates`.
Они имеют смысл временной отметки и координат последнего положения водителя, известного
клиенту. Если они переданы, в ответе, кроме текущего положения водителя, будет также
маршрут до него из положения, указанного клиентом.

Возможные коды ответа:
    * 304, если позицию водителя определить не удалось;
    * 400, если запрос составлен некорректно;
    * 401, если пользователь не авторизован;
    * 404, если заказ или водитель не найдены.

В ответе приходит объект со следующими полями:
    * `timestamp` и `coordinates` - временная отметка и координаты текущего
        (по сведениям бекенда) положения водителя.
    * `start_timestamp` - временная отметка последнего положения водителя,
        известного клиенту. Маршрут строится в промежутке `[start_timestamp, timestamp]`.
    * `route` - список отрезков маршрута от точки в момент `start_timestamp` до точки
        в момент `end_timestamp`. Пуст, если клиент не передал параметры `timestamp` и
        `coordinates` в запросе.

### Пример 1

        {
                "id": "97d4418d5ecf41859da8825cf76059b1",
                "orderid": "080e54aaa2634f569e040250002b5baa"
        }

-

        {
                "coordinates": [
                        37.58888,
                        55.734761
                ],
                "route": [],
                "start_timestamp": "2015-12-01T17:08:18+0300",
                "timestamp": "2015-12-01T17:08:18+0300"
        }

### Пример 2

        {
                "id": "97d4418d5ecf41859da8825cf76059b1",
                "orderid": "080e54aaa2634f569e040250002b5baa",
                "timestamp": "2015-12-01T17:08:18+0300",
                "coordinates": [
                        37.58888,
                        55.734761
                ]
        }

-

        {
                "coordinates": [
                        37.59431,
                        55.74381
                ],
                "route": [{
                        "src": [37.58888, 55.734761],
                        "dst": [37.59431, 55.74381],
                        "distance": 1062.36420
                }],
                "start_timestamp": "2015-12-01T17:08:18+0300",
                "timestamp": "2015-12-01T17:48:18+0300"
        }

### Пример 3 (с явным указанием driverid, тестинг)

        {
                "id": "97d4418d5ecf41859da8825cf76059b1",
                "driverid": "1234_5678",
        }

-

        {
                "coordinates": [
                        37.58888,
                        55.734761
                ],
                "route": [],
                "start_timestamp": "2015-12-01T17:48:18+0300",
                "timestamp": "2015-12-01T17:48:18+0300"
        }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __build_route__ `t: boolean`     строить маршрут (новое плавное движение)
*    __coordinates__ `t: point`     откуда прокладывать маршрут
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __driverid__ `t: string`     идентификатор водителя (для тестинга)
*    __orderid__ `t: uuid4`     идентификатор заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __timestamp__ `t: string`  `f: date-time`   время последнего полученного трека
*    __use_history__ `t: boolean`     включить новое плавное движение

### Допустимые параметры ответа

*   ⋮ __route__ `t: array`     маршрут от указанной точки до текущего положения водителя
    *    __distance__ `t: number`     длина отрезка
    *    __dst__ `t: point`     координаты конца отрезка
        *   ⋮ __response__ `t: point`     объект ответа целиком
    *    __length__ `t: string`     координаты начала отрезка
    *    __points__ `t: array`     длина отрезка
        *    __distance__ `t: number`     длина отрезка
        *    __dst__ `t: point`     координаты конца отрезка
            *   ⋮ __response__ `t: point`     объект ответа целиком
        *    __src__ `t: point`     координаты начала отрезка
            *   ⋮ __response__ `t: point`     объект ответа целиком
    *    __src__ `t: point`     координаты начала отрезка
        *   ⋮ __response__ `t: point`     объект ответа целиком
    *    __time__ `t: string`     координаты конца отрезка
*    __coordinates__ `t: point`     координаты последнего трека водителя
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __direction__ `t: number`     направление движения водителя
*    __driver__ `t: object`     Информация о машине
*    __raw_data__ `t: array`     Список последних координат
    *    __coordinates__ `t: point`     координаты трека водителя
        *   ⋮ __response__ `t: point`     объект ответа целиком
    *    __timestamp__ `t: string`  `f: date-time`   время трека
*    __start_timestamp__ `t: string`  `f: date-time`   время первой точки на маршруте
*    __timestamp__ `t: string`  `f: date-time`   время последнего трека водителя
*    __track__ `t: array`     Последние хранимые координаты водителя
    *    __coordinates__ `t: point`     координаты трека водителя
        *   ⋮ __response__ `t: point`     объект ответа целиком
    *    __direction__ `t: number`     направление движения водителя
    *    __speed__ `t: number`     средняя скорость автомобиля
    *    __timestamp__ `t: string`  `f: date-time`   время трека

<a name="request_taxisearch"></a>
## taxisearch
### Описание

Экран поиска машины на заказ.

Рекомендуется повторять этот запрос через равные промежутки в течение всего поиска машины на заказ.
Параметр `status` укажет момент, когда поиск машины завершился, и следует перейти на другой экран.

Если пользователь при заказе ввел код купона, в поле `coupon` возвращается информация о валидности
и номинале купона.

В поле `request` содержится поле `requirements`, содержащее все исходные требования заказа.

Если заказ оплачивается картой, но в какой-то момент выяснилось, что данная карта
не может использоваться для оплаты, в поле `request` добавляется поле `updated_requirements`
со следующей структурой (поле `requirements` при этом не изменяется):

    [
        {
            'requirement': 'creditcard',
            'value': false,
            'reason': {
                'code': 'UNUSABLE_CARD',
                'text': 'Некий текст для показа пользователю'
            }
        }
    ]

Возможные значения поля `code` (список кодов впоследствии может расширяться):

- UNUSABLE_CARD - карта не может быть использована для оплаты
- UNKNOWN_CARD - данная карта не привязана к аккаунту пользователя

Сервер передаёт клиенту информацию об установленных им (клиентом) ранее
чаевых по заказу в поле `tips`. Поле `available` говорит о том, можно ли
для данного заказа устанавливать размер чаевых.

Если сейчас происходит поиск исполнителя на заказ по повышенному коэффициенту,
то `request` обогощается полем `surge_value`, в котором можно видеть значение
выбранного коэффициента.

Если по мнению сервера поиск слишком затянулся, в ответе придет дополнительное
поле `reorder`, в котором будет содежраться информация, которую нужно показать
клиенту. Если пользователь выбрал одну из опций в `options`, то `decision_id`
нужно передать в ручку `/reorder`.

Если в городе проблема с таксистами, то в ответе может прийти поле `surge`.
Это словарь. Ключи: `decision_id`, строка, которую надо передать в метод `/reorder`,
если пользователь согласится повысить тариф (см. описание поля `reorder`).
`small_icon_label` - текст краткой подписи, при нажатие на которую появляется
диалог суржпрайсинга. `button_label` - текст кнопки-подтверждения готовности
умножить цену на коэффициент. `title, info` - тексты для отображения в диалоге
суржпрайсинга.

Сервер передаёт клиенту возможные причины "Что было не так?" в поле
"supported_feedback_choices". Формат поля такой же, как и в [/cities](cities.md),
 только вместо "cancelled_reason" - "low_rating_reason".

В поле `payment` передается информация о текущем способе оплаты заказа.
Например, для заказа за наличные:
```json
"payment": {
    "type": "cash"
}
```

Для заказа по карте:
```json
"payment": {
    "type": "card",
    "payment_method_id": "card-012345"
}
```

Для заказа по корпоративному счету:
```json
"payment": {
    "type": "corp",
    "payment_method_id": "corp-012345"
}
```

В поле `payment_changes` предаётся информация об изменениях в способе оплаты и причины этих изменений.
Это поле заменяет собой `update_requirements`.

### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1234567890mnopqrstuvwx0987654321"
    }

-

    {
        "status": "search",
        "freecars": [
            [37.588404, 55.733931],
            [38.588404, 54.733931]
        ],
        "busycars": [
            [37.488404, 55.933931],
            [37.188404, 56.733931]
        ],
        "source": [37.588404, 56.733931],
        "request": {
            "due": "2013-04-11T19:58:24+0400",
            "requirements": {
                "check": true
            },
            "route": [
                {
                    "country": "Россия",
                    "fullname": "Россия, Москва, Новосущевская, 1",
                    "geopoint": [
                        33.6,
                        55.1
                    ],
                    "locality": "Москва",
                    "porchnumber": "1",
                    "premisenumber": "1",
                    "thoroughfare": "Новосущевская"
                },
                {
                    "country": "Россия",
                    "fullname": "Россия, Москва, 8 Марта, 4",
                    "geopoint": [
                        33.1,
                        52.1
                    ],
                    "locality": "Москва",
                    "porchnumber": "",
                    "premisenumber": "4",
                    "thoroughfare": "8 Марта"
                }
            ],
        },
        "coupon": {
            "valid": false
        },
        "tips": {
            "type": "percent",
            "value": 0,
            "available": false
        },
        "payment": {
            "type": "cash"
        },
        "payment_changes": [],
        "surge": {
            "title": "Из-за грозы такси в городе сильно загружено.",
            "info": "Включить тариф ×1,8, чтобы увеличить количество доступных водителей?",
            "small_icon_label": "Ускорить поиск",
            "decision_id": "93f3ed871cc54054b64d1b671f99200e",
            "button_label": "Ускорить поиск"
        },
        "supported_feedback_choices": {
            "low_rating_reason": [
                {
                    "name": "driverlate",
                    "label": "Водитель опоздал"
                },
                {
                    "name": "rudedriver",
                    "label": "Грубый водитель"
                },
                {
                    "name": "smellycar",
                    "label": "Запах в машине"
                },
                {
                    "name": "carcondition",
                    "label": "Состояние автомобиля"
                },
                {
                    "name": "badroute",
                    "label": "Ездил кругами"
                },
                {
                    "name": "nochange",
                    "label": "Не было сдачи"
                }
            ]
        }
    }

### Пример безналичного заказа, ставшего наличным

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1234567890mnopqrstuvwx0987654321"
    }

-

    {
        "status": "search",
        "freecars": [
            [37.588404, 55.733931],
            [38.588404, 54.733931]
        ],
        "busycars": [
            [37.488404, 55.933931],
            [37.188404, 56.733931]
        ],
        "source": [37.588404, 56.733931],
        "request": {
            "due": "2013-04-11T19:58:24+0400",
            "requirements": {
                "creditcard": true,
                "check": true
            },
            "updated_requirements": [
                {
                    'requirement': 'creditcard',
                    'value': false,
                    'reason': {
                        'code': 'UNUSABLE_CARD',
                        'text': 'Заказ не может быть оплачен картой, готовьте наличные!'
                    }
                }
            ],
            "route": [
                {
                    "country": "Россия",
                    "fullname": "Россия, Москва, Новосущевская, 1",
                    "geopoint": [
                        33.6,
                        55.1
                    ],
                    "locality": "Москва",
                    "porchnumber": "1",
                    "premisenumber": "1",
                    "thoroughfare": "Новосущевская"
                },
                {
                    "country": "Россия",
                    "fullname": "Россия, Москва, 8 Марта, 4",
                    "geopoint": [
                        33.1,
                        52.1
                    ],
                    "locality": "Москва",
                    "porchnumber": "",
                    "premisenumber": "4",
                    "thoroughfare": "8 Марта"
                }
            ],
        },
        "coupon": {
            "valid": false
        },
        "tips": {
            "type": "percent",
            "value": 0,
            "available": false
        },
        "payment": {
            "type": "card",
            "payment_method_id": "card-12345"
        },
        "payment_changes": [
            {
                "from": {
                    "type": "card",
                    "payment_method_id": "card-12345"
                },
                "to": {
                    "type": "cash",
                },
                "reason": {
                    "code": "UNUSABLE_CARD",
                    "text": "Заказ не может быть оплачен картой, готовьте наличные!"
                }
            }
        ],
        "supported_feedback_choices": {
            "low_rating_reason": [
                {
                    "name": "driverlate",
                    "label": "Водитель опоздал"
                },
                {
                    "name": "rudedriver",
                    "label": "Грубый водитель"
                },
                {
                    "name": "smellycar",
                    "label": "Запах в машине"
                },
                {
                    "name": "carcondition",
                    "label": "Состояние автомобиля"
                },
                {
                    "name": "badroute",
                    "label": "Ездил кругами"
                },
                {
                    "name": "nochange",
                    "label": "Не было сдачи"
                }
            ]
        }
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __orderid__ `t: uuid4`     идентификатор заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __break__ `t: string` `v: user/timeout`    отмена заказа
*    __format_currency__ `t: boolean`      если передан, то в ответе передаем валюты в определенном формате
*    __position__ `t: position`     ?
    *   ⋮ __response__ `t: position`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __cancel_disabled__ `t: boolean`     Отмена заказа запрещена
*   ⋮ __status__ `t: order_status`     статус заказа
    *   ⋮ __response__ `t: order_status`     объект ответа целиком
*    __allowed_changes__ `t: array`     возможные действия по изменению заказа
*    __autoreorder__ `t: object`     уведомление о поиске нового исполнителя
    *    __text__ `t: string`     текст сообщения, которое необходимо отобразить пользователю
*    __block_time__ `t: string`     время, на которое пользователь будет заблокирован
*    __busycars__ `t: array`     координаты занятых машин
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __cancelled_by__ `t: ` `v: park/user`    Инициатор отмены
*    __cost__ `t: number`     стоимость поездки (без учета купона)
*    __cost_as_str__ `t: string`     стоимость (без учета промокода) + валюта (с учетом format_currency)
*    __cost_message__ `t: string`     стоимость поездки текстом
*    __coupon__ `t: coupon_info`     предъявленный к оплате купон
    *   ⋮ __response__ `t: coupon_info`     объект ответа целиком
*    __currency_rules__ `t: currency_rules`     данные о валюте заказа (если клиент запросил)
    *   ⋮ __response__ `t: currency_rules`     объект ответа целиком
*    __discount__ `t: number`     скидка в рублях, если купон валидный
*    __dont_call__ `t: boolean`     значение ранее переданного флага dont_call
*    __dont_sms__ `t: boolean`     не смсить ли пользователю
*    __driver__ `t: object`     информация о водителе и автомобиле
    *    __car__ `t: point`     местоположение машины
        *   ⋮ __response__ `t: point`     объект ответа целиком
    *    __color__ `t: string`     цвет машины
    *    __color_code__ `t: string`     код цвета машины
    *    __forwarding__ `t: forwarding`     информация o переадресованном номере телефона водителя
        *   ⋮ __response__ `t: forwarding`     объект ответа целиком
    *    __model__ `t: string`     модель машины
    *    __name__ `t: string`     имя водителя
    *    __overdue__ `t: boolean`     трек слишком старый
    *    __phone__ `t: phone`     номер телефона водителя
        *   ⋮ __response__ `t: phone`     объект ответа целиком
    *    __plates__ `t: string`     госномер машины
    *    __way_time__ `t: integer`     время водителя в пути до места подачи (или -1, если оно слишком большое)
*    __feedback__ `t: user_feedback`     фидбэк пользователя на заказ
    *   ⋮ __response__ `t: user_feedback`     объект ответа целиком
*    __final_cost__ `t: number`     окончательная стоимость поездки с учетом купона
*    __final_cost_as_str__ `t: string`     стоимость (с учетом промокода) + валюта (с учетом format_currency)
*    __freecars__ `t: array`     координаты свободных машин
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __granted_promotions__ `t: array`     список идентификаторов промо-акций, которые были применены к заказу
*    __higher_class_dialog__ `t: object`     диалог о назначении машины из более высокого класса https://st.yandex-team.ru/TAXIBACKEND-2628
    *   ⋮ __tag__ `t: string`     имя тэга для получения изображения
    *   ⋮ __text__ `t: string`     текст диалога
    *   ⋮ __title__ `t: string`     заголовок диалога
*    __loyal__ `t: boolean`     лояльный пользователь
*    __park__ `t: object`     информация о таксопарке, исполняющем заказ
    *   ⋮ __id__ `t: string`     идентификатор таксопарка
    *   ⋮ __name__ `t: string`     название таксопарка
    *   ⋮ __phone__ `t: phone`     номер телефона диспетчерской (прямой или через шлюз переадресации)
        *   ⋮ __response__ `t: phone`     объект ответа целиком
    *   ⋮ __yamoney__ `t: boolean`     принимаются к оплате Яндекс.Деньги
    *    __forwarding__ `t: forwarding`     информация o переадресованном номере телефона диспетчерской
        *   ⋮ __response__ `t: forwarding`     объект ответа целиком
*    __payment__ `t: payment`     способ оплаты
    *   ⋮ __response__ `t: payment`     объект ответа целиком
*    __payment_changes__ `t: array`     смены метода оплаты
*    __pending_changes__ `t: array`     еще не примененные изменения по заказу
*    __reorder__ `t: reorder_suggestion`     предложение по обновлению требований к заказу
    *   ⋮ __response__ `t: reorder_suggestion`     объект ответа целиком
*    __request__ `t: object`     информация о заказе
    *   ⋮ __comment__ `t: string`     комментарий заказа
    *   ⋮ __due__ `t: string`  `f: date-time`   время подачи
    *   ⋮ __requirements__ `t: requirements_response`     исходные требования в заказе
        *   ⋮ __response__ `t: requirements_response`     объект ответа целиком
    *   ⋮ __route__ `t: array`     маршрут заказа
        *   ⋮ __response__ `t: route_point`     объект ответа целиком
    *    __corp_cost_center__ `t: string`     кост-центр поездки - только для корпоративных пользователей 
    *    __service_level__ `t: service_level`     положения селектора дёшево-комфортно
        *   ⋮ __response__ `t: service_level`     объект ответа целиком
    *    __surge_value__ `t: number`     значение суржпрайсинга для этого заказа
    *    __updated_requirements__ `t: updated_requirements`     требования, измененные в процессе заказа
        *   ⋮ __response__ `t: updated_requirements`     объект ответа целиком
*    __route_sharing_url__ `t: string`     URL для фичи шаринг маршрута
*    __routeinfo__ `t: object`     текущая информация по маршруту
    *    __distance_left__ `t: number`     расстояние до точки назначения в метрах (по данным маршрутизатора)
    *    __positions__ `t: array`     доп. точки по маршруту. Например, точка Б предыдущего заказа при цепочке заказов
        *    __info_key__ `t: string`     ключ описания точки
        *    __point__ `t: point`     точка на карте
            *   ⋮ __response__ `t: point`     объект ответа целиком
    *    __time_left__ `t: number`     ?
*    __source__ `t: point`     точка подачи машины
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __supported_feedback_choices__ `t: supported_feedback_choices`     возможные варианты фидбэка в этом городе
    *   ⋮ __response__ `t: supported_feedback_choices`     объект ответа целиком
*    __surge__ `t: surge`     информация для отображения диалога текущей ставки суржпрайсинга
    *   ⋮ __response__ `t: surge`     объект ответа целиком
*    __tariff__ `t: object`     информация о тарифе
    *   ⋮ __id__ `t: string`     идентификатор тарифа (уникален в пределах таксопарка)
    *   ⋮ __name__ `t: string`     название тарифа
*    __tips__ `t: user_tips`     чаевые, переданные пользователем на заказ (могут быть изменены в зависимости от состояния заказа)
    *   ⋮ __response__ `t: user_tips`     объект ответа целиком
*    __user_ready__ `t: boolean`     Пользователь на кнопку 'Уже выхожу'

<a name="request_translations"></a>
## translations
# Описание

Возвращает массив ключ: значение для заданного набора ключей
 
### Запрос
`POST /3.0/translations/`
```python
{
    "keyset": "cancel_state"
}
```

### Ответ
```python
{
    "cancel_state.free.title": "text",
    "cancel_state.free.message": "text",
    "cancel_state.free.message_support": "text",
    "cancel_state.paid.title": "text",
    # ...
}
```

## Пример
`curl -H "Accept-Language:ru" tc.mobile.yandex.net/3.0/translations -d '`
```json
{
  "keyset": "cancel_state"
}
```
```json
{
 "cancel_state.free.message": "Сейчас отмена бесплатна. После приезда водителя, возможно, придётся платить",
 "cancel_state.free.message_support": "Идите в суппорт",
 "cancel_state.free.title": "Бесплатная отмена",
 "cancel_state.paid.message": "Стоимость отмены зависит от тарифа и времени ожидания. Если вы вынуждены отменить заказ не по вашей вине, выберите пункт \"прошу связаться со мной\" и опишите ситуацию. Мы вернём вам деньги в случае ошибки.",
 "cancel_state.paid.message_support": "Идите в суппорт",
 "cancel_state.paid.title": "Платная отмена"
}
```





### Допустимые параметры запроса

*   ⋮ __keyset__ `t: string`     Идентификатор набора строк

### Допустимые параметры ответа


<a name="request_updatetips"></a>
## updatetips
### Описание

Установка чаевых на заказ.

Пользователь может в любой момент изменить процент чаевых на заказ.

См. также установку чаевых в запросе `/3.0/feedback`.

### Пример

    {
        "id": "1234567890abcdefghijkl0987654321",
        "orderid": "1234567890abcdefghijkl0987654321",
        "tips": {
            "type": "percent",
            "value": 25
        }
    }

    -

    {}

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __orderid__ `t: uuid4`     идентификатор заказа
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __tips__ `t: tips`     чаевые
    *   ⋮ __response__ `t: tips`     объект ответа целиком

### Допустимые параметры ответа


<a name="request_userplacenew"></a>
## userplacenew
### Описание

Создание черновика для нового избранного места. Возвращает объект `place`,
содержащий идентификатор и версию нового объекта.

### Пример

    {
        "id": "300ab85fbcc54eb49438e0e39bab040c"
    }

-

    {
        "place": {
            "id": "560d20857e924d6b8615f6b17d872b34",
            "version": 0,
        }
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __place__ `t: object`     ?
    *   ⋮ __id__ `t: uuid4`     идентификатор избранного адреса
        *   ⋮ __response__ `t: uuid4`     объект ответа целиком
    *   ⋮ __version__ `t: integer`     версия объекта

<a name="request_userplaces"></a>
## userplaces
### Описание

Получение списка избранных адресов пользователя.

### Пример

    {
        "id": "300ab85fbcc54eb49438e0e39bab040c"
    }

-

    {
        "places": [
            {
                "id": "560d20857e924d6b8615f6b17d872b34",
                "version": 1,
                "name": "HOME",
                "address": {
                    "city": "Moscow",
                    "description": "Moscow, Russian Federation",
                    "full_text": "Russian Federation, Moscow, Petrovsky Boulevard, 21",
                    "point": [
                        37.619046,
                        55.767843
                    ],
                    "house": "21",
                    "object_type": "другое",
                    "exact": true,
                    "street": "Petrovsky Boulevard",
                    "country": "Russian Federation",
                    "short_text": "Petrovsky Boulevard, 21",
                    "type": "address"
                }
            }
        ]
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком

### Допустимые параметры ответа

*   ⋮ __places__ `t: array`     список избранных пользовательских мест
    *   ⋮ __address__ `t: object/address`     избранный адрес
        *   ⋮ __response__ `t: object/address`     объект ответа целиком
    *   ⋮ __id__ `t: uuid4`     идентификатор избранного адреса
        *   ⋮ __response__ `t: uuid4`     объект ответа целиком
    *   ⋮ __name__ `t: string`     название места
    *   ⋮ __version__ `t: integer`     текущая версия объекта

<a name="request_userplacesimport"></a>
## userplacesimport
### Описание

Импорт избранных адресов с клиента. Обновляет имеющуюся запись или создает
новую. Чтобы избежать дублирования записей, они склеиваются по составному ключу:

 * name, заголовок адреса
 * full_text, русский полный текст адреса
 * commemnt
 * porchnumber

### Пример

    {
        "id": "300ab85fbcc54eb49438e0e39bab040c",
        "places": [
            {
                "name": "HOME",
                "address": {
                    "description": "Москва, Россия",
                    "full_text": "Россия, Москва, Петровский бульвар, 21",
                    "point": [
                        37.619046,
                        55.767843
                    ],
                    "house": "21",
                    "object_type": "другое",
                    "street": "Петровский бульвар",
                    "short_text": "Петровский бульвар, 21",
                    "exact": true,
                    "city": "Москва",
                    "country": "Россия",
                    "type": "address"
                }
            }
        ]
    }

-

    {}

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __places__ `t: array`     список избранных пользовательских мест
    *   ⋮ __address__ `t: object/address`     избранные адреса
        *   ⋮ __response__ `t: object/address`     объект ответа целиком
    *   ⋮ __name__ `t: string`     название места
    *    __device_stats__ `t: object`     статистика использования адреса, накопленная устройством
        *    __destination__ `t: integer`     ?
        *    __source__ `t: integer`     ?

### Допустимые параметры ответа


<a name="request_userplacesremove"></a>
## userplacesremove
### Описание

Удаление избранных адресов. Если версия одного из объектов не совпадает с
версией, переданной в запросе, запрос завершится с кодом 409 (conflict).

### Пример

    {
        "id": "300ab85fbcc54eb49438e0e39bab040c"
        "places": [
            {
                "id": "560d20857e924d6b8615f6b17d872b34",
                "version": 2
            }
        ]
    }

-

    {
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __places__ `t: array`     список мест на удаление
    *   ⋮ __id__ `t: uuid4`     идентификатор избранного адреса
        *   ⋮ __response__ `t: uuid4`     объект ответа целиком
    *   ⋮ __version__ `t: integer`     текущая версия объекта

### Допустимые параметры ответа


<a name="request_userplacesupdate"></a>
## userplacesupdate
### Описание

Обновление избранных адресов. В запросе необходимо передать текущии версии
редактируемых объектов. Если для какого-то объекта версия не совпадает,
запрос завершится с кодом 409 (conflict).

### Пример

    {
        "id": "300ab85fbcc54eb49438e0e39bab040c",
        "places": [
            {
                "id": "16fd261107aa43eb96582b049d68b1c4",
                "version": 1,
                "name": "HOME",
                "address": {
                    "description": "Москва, Россия",
                    "full_text": "Россия, Москва, Петровский бульвар, 21",
                    "point": [
                        37.619046,
                        55.767843
                    ],
                    "house": "21",
                    "object_type": "другое",
                    "street": "Петровский бульвар",
                    "short_text": "Петровский бульвар, 21",
                    "exact": true,
                    "city": "Москва",
                    "country": "Россия",
                    "type": "address"
                }
            }
        ]
    }

-

    {
    }

### Допустимые параметры запроса

*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __places__ `t: array`     список избранных пользовательских мест
    *   ⋮ __address__ `t: object/address`     избранные адреса
        *   ⋮ __response__ `t: object/address`     объект ответа целиком
    *   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
        *   ⋮ __response__ `t: uuid4`     объект ответа целиком
    *   ⋮ __name__ `t: string`     название места
    *   ⋮ __version__ `t: integer`     текущая версия объекта
    *    __device_stats__ `t: object`     статистика использования адреса, накопленная устройством
        *    __destination__ `t: integer`     ?
        *    __source__ `t: integer`     ?

### Допустимые параметры ответа

*   ⋮ __places__ `t: array`     список мест
    *   ⋮ __id__ `t: uuid4`     идентификатор избранного адреса
        *   ⋮ __response__ `t: uuid4`     объект ответа целиком
    *   ⋮ __version__ `t: integer`     текущая версия объекта

<a name="request_weathersuggest"></a>
## weathersuggest
### Описание

Выдача информации о погодных условиях в заданной точке и рекомендаций по
отображению текущего погодного явления, которое потенциально может
влиять на время подачи и качество сервиса.


### Пример (нет информации о погоде, нет рекомендаций)

    {
        "id": "1234567890abcdefghijkl0987654321",
        "ll": [37.500140, 55.712230],
        "dx": 312
    }

-

    {
    }


### Пример (снег)

    {
        "id": "1234567890abcdefghijkl0987654321",
        "ll": [30.315868, 59.939095],
        "dx": 915
    }

-

    {
        "base_weather_code": "snow",
        "message": "мокрый питерский снег"
    }

### Допустимые параметры запроса

*   ⋮ __dx__ `t: integer`     погрешность местоположения в метрах
*   ⋮ __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*   ⋮ __ll__ `t: point`     центр области поиска
    *   ⋮ __response__ `t: point`     объект ответа целиком

### Допустимые параметры ответа

*    __base_weather_code__ `t: string`     код погодного явления
*    __message__ `t: string`     сопроводительный текст

<a name="request_zoneinfo"></a>
## zoneinfo
### Описание

Получение информации о зоне.

### Пример

    {
      "id": "57a96d8ebc1c4788b4c6f623c319693e", 
      "size_hint": 390, 
      "skin_version": 2, 
      "zone_name": "spb"
    }

-

    {
      "copyright": "© 2011–2016 ООО «Яндекс.Такси»",
      "exact_orders": true,
      "is_beta": false,
      "max_tariffs": [
        {
          "can_be_default": true,
          "class": "econom",
          "description": "Hyundai Solaris, Kia Rio, Ford Focus, Renault Fluence",
          "icon": {
            "size_hint": 9999,
            "url": "https://tc.tst.mobile.yandex.net/static/test-images/598/9127c844-5af3-4459-97b5-7896e2a7beb4"
          },
          "id": "econom",
          "image": {
            "size_hint": 9999,
            "url": "https://tc.tst.mobile.yandex.net/static/test-images/743/24566c24-ee79-47f0-a898-2fef0b664247"
          },
          "is_default": true,
          "name": "Эконом",
          "only_for_soon_orders": false,
          "service_levels": [
            50
          ],
          "supported_requirements": [
            {
              "label": "Некурящий водитель",
              "name": "nosmoking",
              "persistent": false,
              "type": "boolean"
            },
            {
              "label": "Перевозка животного",
              "name": "animaltransport",
              "persistent": false,
              "type": "boolean"
            },
            {
              "label": "Кузов универсал",
              "name": "universal",
              "persistent": false,
              "type": "boolean"
            },
            {
              "label": "Детское кресло...",
              "name": "childchair",
              "persistent": false,
              "select": {
                "caption": "Выберите тип кресла:",
                "options": [
                  {
                    "label": "Бустер",
                    "name": "only_booster",
                    "value": 7
                  }
                ],
                "type": "number"
              },
              "type": "select"
            },
            {
              "label": "Кондиционер",
              "name": "conditioner",
              "persistent": false,
              "type": "boolean"
            },
            {
              "label": "Квитанция об оплате",
              "name": "check",
              "persistent": false,
              "type": "boolean"
            }
          ]
        }
      ],
      "payment_options": {
        "corp": true,
        "coupon": true
      },
      "req_destination": true,
      "support_page": {
        "url": "https://m.taxi.taxi.tst.yandex.ru/help"
      },
      "supported_feedback_choices": {
        "cancelled_reason": [
          {
            "label": "Заказал по ошибке",
            "name": "usererror"
          },
          {
            "label": "Водитель попросил отменить",
            "name": "driverrequest"
          },
          {
            "label": "Слишком долго ждать",
            "name": "longwait"
          },
          {
            "label": "Уехал на другом такси",
            "name": "othertaxi"
          },
          {
            "label": "Водитель ехал в другую сторону",
            "name": "droveaway"
          }
        ]
      },
      "tariffs_url": "https://m.taxi.taxi.tst.yandex.ru/zone-tariff/?id=spb",
      "tz": "+0300"
    }

### Допустимые параметры запроса

*    __id__ `t: uuid4`     идентификатор сессии пользователя
    *   ⋮ __response__ `t: uuid4`     объект ответа целиком
*    __point__ `t: point`     точка
    *   ⋮ __response__ `t: point`     объект ответа целиком
*    __size_hint__ `t: integer`     желаемый размер изображения (смысл зависит от клиента)
*    __skin_version__ `t: integer`     номер версии скина
*    __supports_hideable_tariffs__ `t: boolean`     данные о поддержке клиентом флага is_hidden
*    __zone_name__ `t: string`     название зоны

### Допустимые параметры ответа

*   ⋮ __exact_order_min_timedelta__ `t: integer`     Минимальная разница между текущем временем и временем подачи в секундах
*   ⋮ __exact_order_round_minutes__ `t: integer`     ко скольки минутам округлять время заказа
*   ⋮ __is_beta__ `t: boolean`     зона запущена в тестовом режиме
*   ⋮ __tariffs_url__ `t: string`     ссылка на страницу с тарифами
*    __copyright__ `t: string`     copyright строка
*    __country_code__ `t: string`     Код страны
*    __currency_code__ `t: string`     Код валюты зоны
*    __exact_order_times__ `t: array`     Список интервалов времени для заказа такси, значения в секундах
*    __max_tariffs__ `t: array`     список тарифов
    *   ⋮ __can_be_default__ `t: boolean`     этот тариф может быть заполнен в качестве тарифа по умолчанию
    *   ⋮ __class__ `t: tariff_class`     категория тарифа
        *   ⋮ __response__ `t: tariff_class`     объект ответа целиком
    *   ⋮ __description__ `t: string`     описание тарифа
    *   ⋮ __icon__ `t: image`     изображение для тарифа
        *   ⋮ __response__ `t: image`     объект ответа целиком
    *   ⋮ __id__ `t: string`     идентификатор тарифа
    *   ⋮ __image__ `t: image`     изображение для тарифа
        *   ⋮ __response__ `t: image`     объект ответа целиком
    *   ⋮ __is_default__ `t: boolean`     этот тариф должен быть выбран как тариф по умолчанию (то есть если клиент в первый раз)
    *   ⋮ __name__ `t: string`     название тарифа
    *   ⋮ __only_for_soon_orders__ `t: boolean`     по этому заказу можно делать только soon-заказы
    *   ⋮ __service_levels__ `t: array`     значения service_levels, действительные для тарифа
    *   ⋮ __supported_requirements__ `t: supported_requirements`     требования, которые можно указывать при заказе в этом городе
        *   ⋮ __response__ `t: supported_requirements`     объект ответа целиком
    *    __restrict_by_payment_type__ `t: array`     поддерживаемые типы оплаты для данного тарифа (отсутствие поля означает поддержку всех типов)
        *   ⋮ __response__ `t: payment_method`     объект ответа целиком
    *    __show_onboarding__ `t: boolean`     Показывать или нет заставку onboarding
*    __region_id__ `t: integer`     ID региона для биллинга
*    __req_destination__ `t: boolean`     при заказе из этой зоны обязательно указывать точку назначения
*    __support_page__ `t: object`     Способ связи со службой поддержки для меню клиентского приложения
    *  Вариант 1
        *    __email__ `t: string`     email для связи со службой поддержки
    *  Вариант 2
        *    __url__ `t: string`     URL для webview
*    __support_phone__ `t: string`     телефон службы поддержки
*    __supported_feedback_choices__ `t: supported_feedback_choices`     возможные варианты фидбэка в этой зоне
    *   ⋮ __response__ `t: supported_feedback_choices`     объект ответа целиком
*    __tz__ `t: string`   `r: ^(\+|-|)\d{2}(\:?\d{2})?$`  таймзона

