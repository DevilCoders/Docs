## Создание/изменение договора
Здесь описываются особенности работы ручек [создания](http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x/#!/rent32moderation/createContract) и [изменения](http://realty-gateway-api.vrts-slb.test.vertis.yandex.net/index.html?url=/api/2.x/#!/rent32moderation/updateContract) договора аренды (далее _ДА_). Сущность договора хранится в базе `realty_rent` в в таблице `rent_contract`.

### Общие ошибки
Эти ошибки валидации нужны для корректной генерации pdf-версии ДА.

| Ошибка                | Описание                                                                               |
|-----------------------|----------------------------------------------------------------------------------------|
| MISSED_USER_PASSPORT  | У собственника нет паспортных данных                                                   |
| MISSED_USER_AUTHORITY | У собственника нет данных о доверенности, хотя указан класс договора "по доверенности" |
| MISSED_USER_OGRNIP    | Не указан ОГРНИП, хотя собственник является юр. лицом                                  |

### Создание договора {#create}
При создании договора мы берем [актуальную версию шаблона](https://palma.test.vertis.yandex-team.ru/dictionaries/realty/dochub/renderer/settings) pdf-договора из Palma, записываем ее в `ContractData.template_versions.contract` и дальше используем ее при генерации документа договора аренды.

### Изменение договора {#update}
Возможно только для договоров в статусе `Draft`. Позволяет редактировать комментарий от координатора в `ContractData.manager_answer`.
