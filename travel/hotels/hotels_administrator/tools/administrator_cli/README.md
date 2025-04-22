# CLI Администратора

## Сборка
`ya make -o ~/arc/arcadia`

## Использование

### Общие параметры:
* `env` - окружение администратора
    * dev - отправляем запросы на локально запущенный администратор
    * testing - тестовый администратор
    * prod - продовый администратор
* `port` - (дефолт 29855) GRPC порт администратора
* `timeout` - (дефолт 10 с) таймаут запроса
* `tvm-client-id` - (дефолт 2021364) tvm ID CLI
* `tvm-client-secret` - секрет администратора. Искать здесь: https://yav.yandex-team.ru/secret/sec-01edv01j9eq44zcxpydcp6b30x/explore/versions

### Создать LegalDetails
* `partner-id` - партнер юр. данных
    * PI_TRAVELLINE
    * PI_BNOVO
* `client-id`, `contract-id`, `person-id` - айдишники сущностей в Балансе

Пример запуска:
`./administrator_cli --env prod --tvm-client-secret ***** createLegalDetails --partner-id PI_TRAVELLINE --client-id 1337966112 --contract-id 1873672 --person-id 11996179`

### Обновить LegalDetails
* `legal-details-id` - значение в колонке `legal_details.id`

Пример запуска:
`./administrator_cli --env prod --tvm-client-secret ***** updateLegalDetails --legal-details-id c1f50f79-d705-4574-befb-e820ba681265`

### Поменять статус HotelConnection
* `hotel-code` - Id отеля у партнера
* `partner-id` - партнер
    * PI_TRAVELLINE
    * PI_BNOVO
* `connection-state` - статус подключения
    * CS_NEW
    * CS_PUBLISHING
    * CS_PUBLISHED
    * CS_UNPUBLISHED
    * CS_MANUAL_VERIFICATION
* `unpublished-reason` - [опциональный] причина распубликации отеля
    * IUR_AGENCY
    * IUR_ADDITIONAL_SERVICES
    * IUR_APARTMENTS
    * IUR_HOTEL_INITIATIVE
    * IUR_OTHER

Пример запуска:
`./administrator_cli --env prod --tvm-client-secret ***** changeConnectionStatus --hotel-code 83 --partner-id PI_TRAVELLINE --connection-state CS_UNPUBLISHED --unpublished-reason IUR_OTHER`

### Применить HotelConnectionUpdate
* `connection-update-id` - UUID HotelConnectionUpdate
* `bank-change-mode` - поведение администратора при смене банковских реквизитов без смены юр. лица
    * `create_new` - создаем новые сущности в Балансе (отель переходит на новый контракт)
    * `change_inplace` - **[default]** меняем существующие сущности в Балансе (отель остается на том же контракте, меняются реквизиты плательщика)

Пример запуска с обновлением существующих сущностей в случае если это возможно:
`./administrator_cli --env prod --tvm-client-secret ***** acceptConnectionUpdate ---connection-update-id 4caf84ee-9397-4fbd-afa9-1ea266f22039`
Пример запуска с созданием новых сущностей при смене реквизитов/юр. лица:
`./administrator_cli --env prod --tvm-client-secret ***** acceptConnectionUpdate ---connection-update-id 4caf84ee-9397-4fbd-afa9-1ea266f22039 --bank-change-mode create_new`

### Отклонить HotelConnectionUpdate
* `connection-update-id` - UUID HotelConnectionUpdate

Пример запуска:
`./administrator_cli --env prod --tvm-client-secret ***** rejectConnectionUpdate ---connection-update-id 4caf84ee-9397-4fbd-afa9-1ea266f22039`
