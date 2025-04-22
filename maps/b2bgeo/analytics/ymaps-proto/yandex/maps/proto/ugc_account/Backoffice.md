## Backoffice API 

* **Бэкофис Maps UGC Account** - часть [**Maps UGC Account**][Readme], предназначенная для межсервисного взаимодействия: из пользовательского ui запросы сюда не приходят.
* abc: https://abc.yandex-team.ru/services/maps-core-ugc-backoffice/
* Исходники: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/backoffice

### Headers
### Request requirements
Every request must be pefrormed with TVM `ServiceTicket`

### Headers
* `X-Ya-Service-Ticket`
* Accept: `application/x-protobuf`(default) or `text/x-protobuf`


### Response codes
| HTTP code | Response | Explanation |
|---|---|---
| 200 Ok | empty | Actual for PUT method |
| 201 Created | empty | Actual for PUT method |
| 400 Bad Request |  | Request parameters or body malformed |
| 401 Unauthorized |  | No valid service ticket |
| 403 Forbidden |  | Client does not have access to this object |
| 404 Not Found |  | Handler or assignment id not found |
| 409 Conflict |  | Contribuition modification for a uid is already in progress |
| 429 Too Many Requests  |  | Rps quota exceeded |
| 500 Internal Server Error |  | Contact developers |

### API

#### **/v1/assignments/create**

**Method**   | PUT |
-------------|-|
**Params**   | |
`task_id` | Required, id задания в терминах **Сервисса UGC** |
`ttl` | Optional, `ttl` для задания в секундах. По истечении `ttl` задание перейдёт в статус `expired` и ещё через какое-то время будет удалено. По умолчанию `ttl=4838400`, т.е. 8 недель. При обновлении задания `ttl` выставляется заново относительно момента обновления. |
**Description** | Добавить новые задания. Метод является идемпотентным: при добавлении нового задания **Сервис UGC** получит 201 created. При попытке добавить точно такое же задание - 200 ok. При попытке добавить отличное от существующего задание с тем же `task_id` - 400 bad request. |
**Request Body** | [Task][Backoffice] |
**Response Body** | Достаточно кода ответа |
**Пример запроса**:
```
lang_to_metadata {
  key: "en_US"
  value {
    address_add_assignment {
      uri: "ymapsbm://geo?ll=37.37,55.55&z=17"
    }
  }
}
lang_to_metadata {
  key: "ru_RU"
  value {
    address_add_assignment {
      uri: "ymapsbm://geo?ll=37.37,55.55&z=17"
    }
  }
}
uid: "11111111111"
uid: "22222222222"
ttl: 4838400
```
Через ttl секунд несделанные задания будут удаляться автоматически. По умолчанию ttl составляет 8 недель. ttl считается от момента последнего обновления задания.
**Внимание**: **Сервис UGC** генерирует `task_id` в своём пространстве имён. При добавлении `task_id` не из своего пространства имён **Сервис UGC** получит 400 bad request. Также **Сервис UGC** должен уметь работать с `task_id` в это пространстве имён, если получает `task_id` по api.

#### **/v1/assignments/done**
**Method**   | PUT|
-------------|-|
**Params**   | |
`task_id` | Required, id задания в терминах **Сервиса UGC** |
`uid`     | Required, uid пользователя |
**Description** | **Сервис UGC** отмечает задание как сделанное |
**Response Body** | Достаточно кода ответа |


#### **/v1/assignments/delete**
**Method**   | DELETE|
-------------|-|
**Params**   | |
`task_id` | Required, id задания в терминах **Сервиса UGC** |
`uid`     | Required, uid пользователя |
**Description** | Запрос из **Сервиса UGC**: сервис счёл, что задание больше нерелевантно, и что его не нужно показывать пользователю |
**Response Body** | Достаточно кода ответа |


#### **/v1/assignments/status**
**Method**   | GET|
-------------|-|
**Params**   | |
`task_id` | Required, id задания в терминах **Сервиса UGC** |
`uid`     | Required, uid пользователя |
**Description** | Получить актуальный статус задания: active|done|skipped|expired |
**Response Body** | [AssignmentStatus][Backoffice] |
**Пример ответа**:
```
status: ACTIVE
```


#### **/v1/contributions/modify**
**Method**   | PUT|
-------------|-|
**Params**   | |
`uid` | Required, uid пользователя |
**Description** | Запрос из **Сервиса UGC**: редактирование ленты вклада. Можно удалить, заменить или добавить какое-то событие. _Сценарий 1_: пользователь удалил свою фотографию. Во всех связанных событиях в ленте хотим удалить картинку из превью, заменяем каждое событие на новое. _Сценарий 2_: нужно сагрегировать добавление 10 фотографий по отдельности в одно групповое добавление: в запросе удаляются 10 старых событий, добавляется одно новое. Метод является идемпотентным и транзакционным. При добавлении нового contribution-а **Сервис UGC** получит 201 create. При попытке добавить существующий contribution - 200 ok. При попытке добавить отличный от существующего contribution с тем же `contribution_id` существующий будет заменён на новый. Если в данный момент уже происходит обработка другого запроса modify contributions с тем же `uid` - 409 conflict. |
**Request Body** | [ModifyContributions][Backoffice] |
**Response Body** | Достаточно кода ответа |
**Пример запроса**:
```
modify_contribution {
  delete {
    id: "photo1"
  }
}
modify_contribution {
  delete {
    id: "photo2"
  }
}
modify_contribution {
  upsert {
    contribution {
      contribution_id: "photo12"
      lang_to_metadata {
        key: "en_US"
        value {
          /*contribution type*/ {
            // data that is actual for contribution_id
          }
        }
      }
      timestamp: 1111111111
    }
  }
}
```
**Внимание**: **Сервис UGC** генерирует `contribution_id` в своём пространстве имён. При попытке добавить или изменить `contibution_id` не из своего пространства имён **Сервис UGC** получит 400 bad request. Также **Сервис UGC** должен уметь работать с `contribution_id` в это пространстве имён, если получает `contribution_id` по api.


#### **/v1/link/add**
**Method**   | PUT|
-------------|-|
**Params**   | |
`contribution_id` | Required, id вклада в терминах **Сервиса UGC** |
`task_id`         | Required, id задания в терминах **Сервиса UGC** |
`uid`             | Required, uid пользователя |
**Description** | **Сервис UGC** добавляет связь между вкладом и заданием |
**Response Body** | Достаточно кода ответа |

#### **/v1/link/delete**
**Method**   | DELETE|
-------------|-|
**Params**   | |
`contribution_id` | Required, id вклада в терминах **Сервиса UGC** |
`task_id`         | Required, id задания в терминах **Сервиса UGC** |
`uid`             | Required, uid пользователя |
**Description** | **Сервис UGC** удаляет связь между вкладом и заданием |
**Response Body** | Достаточно кода ответа |


### Guide по обновлению формата данных

#### Добавление новых полей в конкретный тип `Assignment-а`/Contribution`-а.
1. Добавляем новые поля в свой тип `Assignment`-a/`Contribution`-а с сохранением обратной совместимости
2. Заполняем их в UGC-сервисе
3. Ждём, когда клиенты научатся их показывать
4. Profit! **Maps UGC Account** обновлять не нужно.

Maps UGC account не надо пересобирать и перевыкатывать. Он продолжит работать со старой версией библиотеки. Но не сможет учитывать новые поля при ранжировании заданий (ну и ладно).

#### Добавление нового типа `Assignment`-а/`Contribution`-а
1. Заводим новый тип `Assignment`-а/`Contribution`-а (файлы `assignment.proto`/`contribution.proto`)
2. Добавляем его в нужный oneof в тех же файлах
3. Если речь об `Assignment`-е, то учим **Maps UGC Account** учитывать этот тип задания при ранжировании
4. Обновляем [конфиги](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/backoffice/docker/install/etc/template_generator/templates/etc/yandex/maps/ugc_backoffice/ugc_backoffice.stable.conf?rev=r8098185#L140) **Maps UGC Backoffice** во всех окружениях (обычно силами likynushka@).
Для обновления конфигов нужно:
   * завести уникальный неймспейс для новых заданий/contribution-ов, актуальный список ниже
   * завести tvm для сервиса-генератора заданий/contribution-ов
5. Обновляем [конфиги](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_core_ugc_backoffice) ratelimiter-а.
6. Пересобираем и перевыкатываем **Maps UGC Backoffice**
7. Начинаем в UGC сервисе заливать новый тип данных в **Maps UGC Backoffice**. Если сделать это раньше обновления **Maps UGC Backoffice**, то он будет возвращать 400 bad request
8. Ждём, когда клиенты научатся показывать новый тип данных
9. Profit!


#### Несовместимые изменения для определённого типа задания
Делаются добавлением нового типа задания с новым номером поля:
1. Добавляем новый тип задания
2. Генератор генерирует задания разных типов: старой версии и новой. У одинаковых по смыслу заданий будет разный `task_id`.
3. Клиент использует тот тип, который умеет отображать.

Аналогично для несовместимых изменений определённого типа вклада.


### Существующие данные

На управление каждым типом задания/contribution-а имеет право только конкретный сервис-генератор. К этому заданию/contribution-у привязывается уникальный префикс. Сервис-генератор обязан генерировать id с этим префиксом, т.е. в своём пространстве имён. При попытке создать данные с некорректным id он получит http 400 bad request

#### Contribution-ы

 Тип | Префикс | metadata_id | abc| пример id |
-----|---------|-------------|----|------------|
[ContributedPhoto](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/contributions/photo.proto)| pht | 1 | [maps-core-photos](https://abc.yandex-team.ru/services/2039/)| pht:111aaa
[RideContribution](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/contributions/mrc_ride.proto)| mrc_ride | 2 | [maps-core-nmaps-mrc-lt](https://abc.yandex-team.ru/services/5375/)| mrc_ride:111aaa
[BaseMapContribution](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/contributions/feedback.proto)| fb | 3 | [maps-core-feedback-api](https://abc.yandex-team.ru/services/31141/)| fb:111aaa
[OrganizationContribution](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/contributions/feedback.proto)| fb | 4 | [maps-core-feedback-api](https://abc.yandex-team.ru/services/31141/)| fb:111aaaa
[RouteContribution](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/contributions/feedback.proto)| fb | 5 | [maps-core-feedback-api](https://abc.yandex-team.ru/services/31141/)| fb:111aaa

#### Assignment-ы

 Тип | Префикс | metadata_id| abc| Пример id | Описание|
-----|---------|------------|----|-----------|---------|
[AddressAddAssignment](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/assignments/address_add.proto)| address_add | 1 | [maps-core-feedback-api](https://abc.yandex-team.ru/services/31141/)<br>[maps-core-feedback-geodata-surveys](https://abc.yandex-team.ru/services/maps-core-feedback-geodata-surveys/)| address_add:111aaa| Задание на добавление адреса: показываем пользователю здание без адреса, просим ввести адрес
[OrganizationEditStatusAssignment](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/assignments/organization_edit_status.proto)| os | 2 | [maps-core-feedback-api](https://abc.yandex-team.ru/services/31141/)<br>[maps-core-feedback-geodata-surveys](https://abc.yandex-team.ru/services/maps-core-feedback-geodata-surveys/)| os:111aaa | Уточнение статуса организации: показываем пользователю организацию, спрашиваем, открыта ли она
[PedestrianAssignment](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/assignments/pedestrian.proto)| mrc_pedestrian | 3 | [maps-core-nmaps-tasks-realtime](https://abc.yandex-team.ru/services/maps-core-nmaps-tasks-realtime/)<br>[maps-core-nmaps-mrc-lt](https://abc.yandex-team.ru/services/maps-core-nmaps-mrc-lt/) | mrc_pedestrian:43118 |
[BarriersEditAssignment](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/assignments/barriers_edit.proto)| barriers_edit | 4 | [maps-core-feedback-api](https://abc.yandex-team.ru/services/31141/)<br>[maps-core-feedback-geodata-surveys](https://abc.yandex-team.ru/services/maps-core-feedback-geodata-surveys/) | barriers_edit:12322 | Показываем пользователю карту с отмеченным известным нам шлагбаумом, спрашиваем, верно ли он расположен
[GatesEditAssignment](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/assignments/gates_edit.proto)| gates_edit | 5 | [maps-core-feedback-api](https://abc.yandex-team.ru/services/31141/)<br>[maps-core-feedback-geodata-surveys](https://abc.yandex-team.ru/services/maps-core-feedback-geodata-surveys/) | gates_edit:345243 | Показываем пользователю карту с отмеченной известной нам калиткой, спрашиваем, верно ли она расположена
[EntrancesEditAssignment](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/assignments/entrances_edit.proto)| entrances_edit | 6 | [maps-core-feedback-api](https://abc.yandex-team.ru/services/31141/)<br>[maps-core-feedback-geodata-surveys](https://abc.yandex-team.ru/services/maps-core-feedback-geodata-surveys/) | entrances_edit:12321 | Показываем пользователю карту со зданием и подъездами в нём. Просим проверить местоположение/названия и добавить отсутствующие подъезды
[SettlementSchemeAssignment](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/assignments/settlement_scheme.proto)| settlement_scheme | 7 | [maps-core-feedback-api](https://abc.yandex-team.ru/services/31141/)<br>[maps-core-feedback-geodata-surveys](https://abc.yandex-team.ru/services/maps-core-feedback-geodata-surveys/) | settlement_scheme:121 | Просим пользователя отправить схему СНТ

[Backoffice]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/backoffice.proto
[Readme]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/Readme.md
