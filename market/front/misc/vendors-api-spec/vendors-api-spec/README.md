# Спецификация API вендоров

## Как читать спецификацию

### Условные обозначения
  - **имяОбязательногоПоля** `<Тип>` - описание поля
  - имяНеобязательногоПоля `значение1|значение2` - описание поля
    - *так записывается комментарий*

### Соглашения
- Необязательное поле может отсутствовать в выдаче
- Если поле присутствует и имеет значение `null`, об этом сказано отдельно

## Базовые структуры данных

### Структура ответа

Выдача всех ручек должна содержать три поля:
  - **meta** `<Object>` – мета-информация о запросе
    - **host** `<String>` - имя хоста с которого возвращается ответ
    - **health** `<Object>` - содержит информацию о здоровье критических узлов в формате "ИМЯ_КОМПОНЕНТА":"СТАТУС". 
    "СТАТУС" может принимать одно из значений "GREEN"|"RED", причем, "GREEN" - компонент работает в штатном режиме, "RED" - компонент НЕ работает в штатном режиме.
      - **balance** `<Enum>` "GREEN"|"RED", при статусе "RED" значения берутся из "долгого" кеша и могут быть неактуальны, запись в баланс невозможна  
      - **staff** `<Enum>` "GREEN"|"RED", при статусе "RED" значения берутся из "долгого" кеша и могут быть неактуальны  
  - result `<Object>` – собственно результат работы ручки
    - сейчас в результате всегда есть обязательное поле **item**, которое содержит все остальные данные
  - errors `<Array[Object]>` – список ошибок
    - *имеет ли смысл делать список ошибок, или можно обойтись одной?*

В ответе всегда есть поле `meta` и одно из полей `errors` и `result` (*не запрещается наличие и обоих полей `errors` и `result`*). Ответ считается ошибкой, если есть поле `errors`, при этом статус-код должен отличаться от 200.

### Абстрактные ошибки

#### Базовая структура **Error**

1. Имеет поля
  - **statusCode** `<Integer>` – численный код ошибки от 400 до 500 (статус-код)
  - **code** `<Enum>` - мнемонический код ошибки (дополняет `statusCode`)
  - **message** `<String>` – сообщение
  - errorString `<String>` – внутренний код ошибки (MBI-encoded)
  - details `<Object>`
    - [key]: [value] – набор параметров, специфичных для этой ошибки

### Ошибки сервантлета

#### Несуществующая ручка
  - statusCode: `404`
  - code: `RESOURCE_NOT_FOUND`
  - message: `The resource %resource is not present`

### Стандартные ошибки

Ошибки, которые могут возникнуть (и должны быть обработаны) в любой ручке

#### Ошибка неавторизованного доступа
  - statusCode: `403`
  - code: `UNAUTHORIZED`
  - message: ???

#### Ошибка сервиса
  - statusCode: `500`
  - code: `INTERNAL_ERROR`
  - message: ???
  - details: stacktrace

#### Метод не поддерживается
  - statusCode: `405`
  - code: `HTTP_METHOD_NOT_SUPPORTED`
  - message: `Request method '%method' not supported`

### Другие общие ошибки

Виды ошибок, общие для некоторых ручек

#### Несуществующий объект данных

Для использования в ручках `/collection/[id]/...`

  - statusCode: `404`
  - code: `ENTITY_NOT_FOUND`
  - message: `The %entity_type with specified ID was not found`

#### Неверные параметры вызова

Для ручек с требованиями к наличию/формату параметров и их проверкой

  - statusCode: `400`
  - code: `BAD_PARAM`
  - message: ???
  - details - список неверных/отсутствующих параметров
    - [param]: [code] - `MISSING|INVALID|ALREADY_EXISTS`
    

#### Есть активные отключения

Для ручек с требованием к отсутствию текущих активных отключений по продуктам (AKA услуги, AKA датасорцы)

  - statusCode: 403
  - code: `ACTIVE_CUTOFFS`
  - message: `The vendor has active cutoffs for product '<product name>': <details>`

## Под вопросом
  1. Ручки
     1. Ручка для сбора фидбека (шлёт информацию об ошибке на нашу ручку)
  1. Добавление бренда к заявке (???)
  1. Добавить признак активности магазина

## Список Ресурсов

| Ресурс     | Назначение        |
|------------|-------------------|
| [GET /vendors](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors#get-vendors)  | Получение списка карточек вендоров |
| [POST /vendors](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors#post-vendors)  | Создание новой карточки вендора |
| [GET /vendors/[vendorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D#get-vendorsvendorid)  | Получение карточки вендора |
| [PUT /vendors/[vendorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D#put-vendorsvendorid)  | Редактирование информации о вендоре |
| [POST /vendors/[vendorId]/recommended](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended#post-vendorsvendoridrecommended)  | Добавление услуги "Рекомендованные магазины" вендору по его vendorId |
| [GET /vendors/[vendorId]/recommended](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended#get-vendorsvendoridrecommended)  | Получение информации об услуге "Рекомендованные магазины" вендора по его vendorId |
| [PUT /vendors/[vendorId]/recommended](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended#put-vendorsvendoridrecommended)  | Редактирование услуги "Рекомендованные магазины" вендора по его vendorId |
| [GET /vendors/[vendorId]/recommended/bid](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/bid#get-vendorsvendoridrecommendedbid)  | Получение текущей общей ставки услуги "Рекомендованные магазины" для выбранной карточки |
| [PUT /vendors/[vendorId]/recommended/bid](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/bid#put-vendorsvendoridrecommendedbid)  | Изменение текущей общей ставки услуги "Рекомендованные магазины" для выбранной карточки |
| [GET /vendors/[vendorId]/recommended/blacklist](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/blacklist#get-vendorsvendoridrecommendedblacklist)  | Получение магазинов из "чёрного списка" услуги "Рекомендованные магазины" |
| [POST /vendors/[vendorId]/recommended/blacklist](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/blacklist#post-vendorsvendoridrecommendedblacklist)  | Добавление магазинов в чёрный список услуги "Рекомендованные магазины" |
| [DELETE /vendors/[vendorId]/recommended/blacklist/[shopId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/blacklist/%5BshopId%5D#delete-vendorsvendoridrecommendedblacklistshopid)  | Удаление магазина из чёрного списка услуги "Рекомендованные магазины" |
| [PUT /vendors/[vendorId]/recommended/placement](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/placement#put-vendorsvendoridrecommendedplacement)  | Изменение (снятие/включение) размещения услуги "Рекомендованные магазины" |
| [GET /vendors/[vendorId]/recommended/shops](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/shops#get-vendorsvendoridrecommendedshops)  | Получение магазинов, привязанных к вендору |
| [POST /vendors/[vendorId]/recommended/shops](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/shops#post-vendorsvendoridrecommendedshops)  | Привязка магазинов к вендору |
| [DELETE /vendors/[vendorId]/recommended/shops/[shopId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/shops/%5BshopId%5D#delete-vendorsvendoridrecommendedshopsshopid)  | Отвязка магазина |
| [PUT /vendors/[vendorId]/recommended/shops/[shopId]/bid](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/shops/%5BshopId%5D/bid#put-vendorsvendoridrecommendedshopsshopidbid)  | Изменение ставки магазина |
| [DELETE /vendors/[vendorId]/recommended/shops/[shopId]/bid](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/shops/%5BshopId%5D/bid#delete-vendorsvendoridrecommendedshopsshopidbid)  | Сброс ставки магазина на дефолтную |
| [POST /vendors/[vendorId]/recommended/shops/bids](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/shops/bids#post-vendorsvendoridrecommendedshopsbids)  | Изменение ставок магазинов |
| [GET /vendors/[vendorId]/recommended/stats/[stat]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/stats#get-vendorsvendoridrecommendedstatsstat)  | Статистика по рекомендованным магазинам |
| [GET /vendors/[vendorId]/recommended/stats/[stat]/download](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/stats#get-vendorsvendoridrecommendedstatsstatdownload)  | Скачивание статистики по рекомендованным магазинам |
| [GET /vendors/[vendorId]/recommended/tariffs](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/tariffs#get-vendorsvendoridrecommendedtariffs)  | Получение текущего тарифа услуги "Рекомендованные магазины" для вендора |
| [POST /vendors/[vendorId]/recommended/tariffs](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/tariffs#post-vendorsvendoridrecommendedtariffs)  | Добавление/изменение следующего тарифа услуги "Рекомендованные магазины" для вендора |
| [GET /vendors/[vendorId]/recommended/categories/blacklist](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/categories/blacklist#get-vendorsvendoridrecommendedcategoriesblacklist)  | Получение списка категорий, заблокированных вендором |
| [PUT /vendors/[vendorId]/recommended/categories/blacklist](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended/categories/blacklist#put-vendorsvendoridrecommendedcategoriesblacklist)  | Установка нового списка заблокированных категорий для вендора |
| [POST /vendors/[vendorId]/brandEditRequests](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/brandEditRequests#post-vendorsvendoridbrandeditrequests)  | Создание вендором заявки на редактирование бренда |
| [GET /vendors/[vendorId]/brandEditRequests/last](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/brandEditRequests/last#get-vendorsvendoridbrandeditrequestslast)  | Получение вендором своей последней заявки на редактирование бренда |
| [GET /categories](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/categories#get-categories)| Поиск по категориям |
| [GET /clients/[ID]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/clients/%5BID%5D#get-clientsid)| Информация о клиенте Баланса |
| [POST /entries](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/entries#post-entries)  | Добавление заявки |
| [GET /entries](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/entries#get-entries)  | Получение списка заявок |
| [GET /entries/[ID]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/entries/%5BID%5D#get-entriesid)  | Получение данных заявки |
| [PUT /entries/[ID]/status](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/entries/%5BID%5D/status#put-entriesidstatus)  | Изменение статуса заявки |
| [GET /brands](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/brands#get-brands)  | Получение списка брендов |
| [GET /authoritiesByVendor/[target_uid]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/roles#get-authoritiesbyvendortarget_uid)  | Получение словаря из ролей пользователя в список вендоров |
| [GET /authorities/[target_uid]/vendor/[vendorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/roles#get-authoritiestarget_uidvendorvendorid)  | Чтение списка ролей пользователя для конкретного вендора |
| [GET /authorities/uids/vendor/[vendorId]/role/[role]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/roles#get-authoritiesuidsvendorvendoridrolerole)  | Возвращает список uid-ов пользователей обладающих указанной ролью для заданного вендора |
| [PUT /authorities/uids/vendor/[vendorId]/role/[role]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/roles#put-authoritiesuidsvendorvendoridrolerole)  | Устанавливает список uid-ов пользователей обладающих указанной ролью для заданного вендора |
| [PUT /authorities/[target_uid]/vendor/[vendorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/roles#put-authoritiestarget_uidvendorvendorid)  | Добавление списка ролей пользователю для вендора |
| [DELETE /authorities/[target_uid]/vendor/[vendorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/roles#delete-authoritiestarget_uidvendorvendorid)  | Удаление списка ролей пользователя для вендора |
| [GET /authorities](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/roles#get-authorities)  | Получение списка всех возможных ролей |
| [GET /permissions](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/roles#get-permissions)  | Получение списка всех возможных разрешений |
| [GET /permissionsByVendor/[target_uid]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/roles#get-permissionsbyvendortarget_uid)  | Получение словаря из разрешений пользователя в список вендоров |
| [GET /tariffs/brandzone](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/tariffs/brandzone#get-tariffsbrandzone)  | Получение списка тарифов услуги "Бренд-зона" |
| [GET /tariffs/recommended](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/tariffs/recommended#get-tariffsrecommended)  | Получение списка тарифов услуги "Рекомендованные магазины" |
| [GET /brandEditRequests](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/brandEditRequests#get-brandeditrequests)  | Получение модератором списка заявок на редактирование бренда |
| [GET /brandEditRequests/[ID]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/brandEditRequests/%5BID%5D#get-brandeditrequestsid)  | Получение модератором конкретной заявки на редактирование бренда |
| [PUT /brandEditRequests/[ID]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/brandEditRequests/%5BID%5D#put-brandeditrequestsid)  | Редактирование\Закрытие модератором конкретной заявки на редактирование бренда |
| [DELETE /brandEditRequests/[ID]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/brandEditRequests/%5BID%5D#delete-brandeditrequestsid)  | Удаление менеджером конкретной заявки на редактирование бренда |
| [POST /brandEditRequests/[ID]/revert](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/brandEditRequests/%5BID%5D/revert#post-brandeditrequestsidrevert)  | Создание модератором корректирующей заявки на редактирование бренда |
| [GET /brandEditRequests/retry](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/brandEditRequests/retry#get-brandeditrequestsretry)  | Попытка повторно отправить заявки на редактирование бренда в MBO |
| [POST /imageConverter/url](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/imageConverter/url#post-imageconverterurl)  | Конвертация URL изображения в BASE64 PNG |
| [POST /imageConverter/multipart](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/imageConverter/multipart#post-imageconvertermultipart)  | Конвертация файла изображения в BASE64 PNG |
| [POST /vendors/[vendorId]/modelbids](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelbids#post-vendorsvendorIdmodelbids)  | Добавление услуги "Управление ставками на модели" вендору по его vendorId |
| [GET  /vendors/[vendorId]/modelbids](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelbids#get-vendorsvendorIdmodelbids)  | Получение информации об услуге "Управление ставками на модели" вендора по его vendorId |
| [PUT /vendors/[vendorId]/modelbids](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelbids#put-vendorsvendorIdmodelbids)  | Изменение информации об услуге "Управление ставками на модели" вендора по его vendorId |
| [POST /vendors/[vendorId]/modelbids/bids](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelbids/bids#post-vendorsvendorIdmodelbidsbids)  | Получение данных из Репорта по фильтру и ставок по моделям из Биддинга |
| [PUT /vendors/[vendorId]/modelbids/bids](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelbids/bids#post-vendorsvendorIdmodelbidsbids)  | Установка ставок на модели (или категории) в биддинг для выбранного вендора |
| [DELETE /vendors/[vendorId]/modelbids/bids](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelbids/bids#delete-vendorsvendorIdmodelbidsbids)  | Сброс ставок на модели (или категории) для выбранного вендора |
| [PUT /vendors/[vendorId]/modelbids/placement](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelbids/placement#put-vendorsvendoridmodelbidsplacement)  | Изменение (снятие/включение) размещения услуги "Управление ставками на модели" |
| [GET /vendors/[vendorId]/modelbids/stats/[stat]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelbids/stats#get-vendorsvendoridmodelbidsstatsstat)  | Статистика по ставкам на модели |
| [GET /vendors/[vendorId]/modelbids/stats/[stat]/download](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelbids/stats#get-vendorsvendoridmodelbidsstatsstat)  | Скачивание статистики по ставкам на модели |
| [GET /vendors/[vendorId]/modelbids/promotion/models](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelbids/promotion)  | Получение моделей, исторической информации по кликам, заказам и показам и прогнозу по их категориям |
| [GET /vendors/[vendorId]/modelbids/promotion/categories/[categoryId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelbids/promotion)  | Получение исторических данных и прогноза по потраченным средствам, кликам, показам и заказам в категории |
| [GET /vendors/[vendorId]/modelEdit/params/byCategory](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/params#get-vendorsvendoridmodeleditparamsbycategory)  | Получение параметров для категории по hid |
| [GET /vendors/[vendorId]/modelEdit/params/byModel](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/params#get-vendorsvendoridmodeleditparamsbymodel)  | Получение параметров модели по modelId со значениями из репорта |
| [GET /vendors/[vendorId]/modelEdit/params/colors](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/params/colors#get-vendorsvendoridmodeleditparamscolors)  | Получение вендорских цветов |
| [GET /vendors/[vendorId]/modelEdit/params/colors/[colorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/params/colors/%5BcolorId%5D#get-vendorsvendoridmodeleditparamscolorscolorid)  | Получение вендорского цвета по его идентификатору |
| [POST /vendors/[vendorId]/modelEdit/params/colors](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/params/colors#post-vendorsvendoridmodeleditparamscolors)  | Создание вендорского цвета |
| [PUT /vendors/[vendorId]/modelEdit/params/colors/[colorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/params/colors/%5BcolorId%5D#put-vendorsvendoridmodeleditparamscolorscolorid)  | Изменение существующего вендорского цвета |
| [DELETE /vendors/[vendorId]/modelEdit/params/colors/[colorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/params/colors/%5BcolorId%5D#delete-vendorsvendoridmodeleditparamscolorscolorid)  | Удаление существующего вендорского цвета |
| [GET /vendors/[vendorId]/modelEdit/params/sku](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/params/sku#get-vendorsvendoridmodeleditparamssku)  | Получение списка SKU модели |
| [GET /vendors/[vendorId]/modelEdit/params/sku/[skuId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/params/sku/%5BskuId%5D#get-vendorsvendoridmodeleditparamsskuskuid)  | Получение SKU модели по его идентификатору |
| [POST /vendors/[vendorId]/modelEdit/params/sku](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/params/sku#post-vendorsvendoridmodeleditparamssku)  | Создание нового SKU модели |
| [PUT /vendors/[vendorId]/modelEdit/params/sku/[skuId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/params/sku/%5BskuId%5D#put-vendorsvendoridmodeleditparamsskuskuid)  | Изменение существующего SKU модели |
| [DELETE /vendors/[vendorId]/modelEdit/params/sku/[skuId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/params/sku/%5BskuId%5D#delete-vendorsvendoridmodeleditparamsskuskuid)  | Удаление существующего SKU модели |
| [POST /vendors/[vendorId]/modelEdit/requests](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/requests#post-vendorsvendoridmodeleditrequests)  | Создание заявки на создание/изменение модели |
| [GET /vendors/[vendorId]/modelEdit/requests](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/requests#get-vendorsvendoridmodeleditrequests)  | Получение списка заявок на создание/изменение модели |
| [GET /vendors/[vendorId]/modelEdit/requests/[requestId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/requests/%5BrequestId%5D#get-vendorsvendoridmodeleditrequestsrequestid)  | Получение заявки на создание/изменение модели |
| [PUT /vendors/[vendorId]/modelEdit/requests/[requestId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/requests/%5BrequestId%5D#put-vendorsvendoridmodeleditrequestsrequestid)  | Изменение заявки на создание/изменение модели |
| [DELETE /vendors/[vendorId]/modelEdit/requests/[requestId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/requests/%5BrequestId%5D#delete-vendorsvendoridmodeleditrequestsrequestid)  | Удаление заявки на создание/изменение модели |
| [GET /vendors/[vendorId]/modelEdit/requests/[requestId]/comments](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/requests/%5BrequestId%5D/comments#get-vendorsvendoridmodeleditrequestsrequestidcomments)  | Получение комментариев к заявке на создание/изменение модели |
| [GET /vendors/[vendorId]/modelEdit/feeds](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/feeds#get-vendorsvendoridmodeleditfeeds)  | Получение заданного вендором списка файлов с данными о моделях |
| [POST /vendors/[vendorId]/modelEdit/feeds](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/feeds#post-vendorsvendoridmodeleditfeeds)  | Сохранение заданного вендором списка файлов с данными о моделях |
| [GET /vendors/[vendorId]/modelEdit/feeds/reports](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/feeds/reports#get-vendorsvendoridmodeleditfeedsreports)  | Получение отчётов по обработке файлов с данными о моделях |
| [GET /vendors/[vendorId]/modelEdit/feeds/templates](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelEdit/feeds#get-vendorsvendoridmodeleditfeedstemplates) | Получение шаблона файла с данными о моделях (для категории) |
| [GET /agencies/[agencyId]/modelEdit/params/byCategory](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/params#get-agenciesagencyidmodeleditparamsbycategory)  | Получение параметров для категории по hid (для агентств) |
| [GET /agencies/[agencyId]/modelEdit/params/byModel](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/params#get-agenciesagencyidmodeleditparamsbymodel)  | Получение параметров модели по modelId со значениями из репорта (для агентств) |
| [POST /agencies/[agencyId]/modelEdit/requests](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/requests#post-agenciesagencyidmodeleditrequests)  | Создание заявки на создание/изменение модели (для агентств) |
| [GET /agencies/[agencyId]/modelEdit/requests](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/requests#get-agenciesagencyidmodeleditrequests)  | Получение списка заявок на создание/изменение модели (для агентств) |
| [GET /agencies/[agencyId]/modelEdit/requests/[requestId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/requests/%5BrequestId%5D#get-agenciesagencyidmodeleditrequestsrequestid)  | Получение заявки на создание/изменение модели (для агентств) |
| [PUT /agencies/[agencyId]/modelEdit/requests/[requestId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/requests/%5BrequestId%5D#put-agenciesagencyidmodeleditrequestsrequestid)  | Изменение заявки на создание/изменение модели (для агентств) |
| [DELETE /agencies/[agencyId]/modelEdit/requests/[requestId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/requests/%5BrequestId%5D#delete-agenciesagencyidmodeleditrequestsrequestid)  | Удаление заявки на создание/изменение модели (для агентств) |
| [GET /agencies/[agencyId]/modelEdit/requests/[requestId]/comments](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/requests/%5BrequestId%5D/comments#get-agenciesagencyidmodeleditrequestsrequestidcomments)  | Получение комментариев к заявке на создание/изменение модели (для агентств) |
| [GET /agencies/[agencyId]/modelEdit/params/colors](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/params/colors#get-agenciesagencyidmodeleditparamscolors)  | Получение вендорских цветов |
| [GET /agencies/[agencyId]/modelEdit/params/colors/[colorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/params/colors/%5BcolorId%5D#get-agenciesagencyidmodeleditparamscolorscolorid)  | Получение вендорского цвета по его идентификатору |
| [POST /agencies/[agencyId]/modelEdit/params/colors](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/params/colors#post-agenciesagencyidmodeleditparamscolors)  | Создание вендорского цвета |
| [PUT /agencies/[agencyId]/modelEdit/params/colors/[colorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/params/colors/%5BcolorId%5D#put-agenciesagencyidmodeleditparamscolorscolorid)  | Изменение существующего вендорского цвета |
| [DELETE /agencies/[agencyId]/modelEdit/params/colors/[colorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/params/colors/%5BcolorId%5D#delete-agenciesagencyidmodeleditparamscolorscolorid)  | Удаление существующего вендорского цвета |
| [GET /agencies/[agencyId]/modelEdit/params/sku](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/params/sku#get-agenciesagencyidmodeleditparamssku)  | Получение списка SKU модели |
| [GET /agencies/[agencyId]/modelEdit/params/sku/[skuId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/params/sku/%5BskuId%5D#get-agenciesagencyidmodeleditparamsskuskuid)  | Получение SKU модели по его идентификатору |
| [POST /agencies/[agencyId]/modelEdit/params/sku](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/params/sku#post-agenciesagencyidmodeleditparamssku)  | Создание нового SKU модели |
| [PUT /agencies/[agencyId]/modelEdit/params/sku/[skuId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/params/sku/%5BskuId%5D#put-agenciesagencyidmodeleditparamsskuskuid)  | Изменение существующего SKU модели |
| [DELETE /agencies/[agencyId]/modelEdit/params/sku/[skuId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/agencies/%5BagencyId%5D/modelEdit/params/sku/%5BskuId%5D#delete-agenciesagencyidmodeleditparamsskuskuid)  | Удаление существующего SKU модели |
| [GET /shops/[shopId]/modelEdit/params/byCategory](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/params#get-shopsshopIdmodeleditparamsbycategory)  | Получение параметров для категории по hid |
| [GET /shops/[shopId]/modelEdit/params/byModel](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/params#get-shopsshopIdmodeleditparamsbymodel)  | Получение параметров модели по modelId со значениями из репорта |
| [POST /shops/[shopId]/modelEdit/requests](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/requests#post-shopsshopIdmodeleditrequests)  | Создание заявки на создание/изменение модели |
| [GET /shops/[shopId]/modelEdit/requests](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/requests#get-shopsshopIdmodeleditrequests)  | Получение списка заявок на создание/изменение модели |
| [GET /shops/[shopId]/modelEdit/requests/[requestId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/requests/%5BrequestId%5D#get-shopsshopIdmodeleditrequestsrequestid)  | Получение заявки на создание/изменение модели |
| [PUT /shops/[shopId]/modelEdit/requests/[requestId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/requests/%5BrequestId%5D#put-shopsshopIdmodeleditrequestsrequestid)  | Изменение заявки на создание/изменение модели |
| [DELETE /shops/[shopId]/modelEdit/requests/[requestId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/requests/%5BrequestId%5D#delete-shopsshopIdmodeleditrequestsrequestid)  | Удаление заявки на создание/изменение модели |
| [GET /shops/[shopId]/modelEdit/requests/[requestId]/comments](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/requests/%5BrequestId%5D/comments#get-shopsshopIdmodeleditrequestsrequestidcomments)  | Получение комментариев к заявке на создание/изменение модели |
| [GET /shops/[shopId]/modelEdit/params/colors](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/params/colors#get-shopsshopIdmodeleditparamscolors)  | Получение вендорских цветов |
| [GET /shops/[shopId]/modelEdit/params/colors/[colorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/params/colors/%5BcolorId%5D#get-shopsshopIdmodeleditparamscolorscolorid)  | Получение вендорского цвета по его идентификатору |
| [POST /shops/[shopId]/modelEdit/params/colors](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/params/colors#post-shopsshopIdmodeleditparamscolors)  | Создание вендорского цвета |
| [PUT /shops/[shopId]/modelEdit/params/colors/[colorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/params/colors/%5BcolorId%5D#put-shopsshopIdmodeleditparamscolorscolorid)  | Изменение существующего вендорского цвета |
| [DELETE /shops/[shopId]/modelEdit/params/colors/[colorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/params/colors/%5BcolorId%5D#delete-shopsshopIdmodeleditparamscolorscolorid)  | Удаление существующего вендорского цвета |
| [GET /shops/[shopId]/modelEdit/params/sku](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/params/sku#get-shopsshopIdmodeleditparamssku)  | Получение списка SKU модели |
| [GET /shops/[shopId]/modelEdit/params/sku/[skuId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/params/sku/%5BskuId%5D#get-shopsshopIdmodeleditparamsskuskuid)  | Получение SKU модели по его идентификатору |
| [POST /shops/[shopId]/modelEdit/params/sku](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/params/sku#post-shopsshopIdmodeleditparamssku)  | Создание нового SKU модели |
| [PUT /shops/[shopId]/modelEdit/params/sku/[skuId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/params/sku/%5BskuId%5D#put-shopsshopIdmodeleditparamsskuskuid)  | Изменение существующего SKU модели |
| [DELETE /shops/[shopId]/modelEdit/params/sku/[skuId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/shops/%5BshopId%5D/modelEdit/params/sku/%5BskuId%5D#delete-shopsshopIdmodeleditparamsskuskuid)  | Удаление существующего SKU модели |
| [GET /licensors/[licensorId]/modelEdit/params/byCategory](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/params#get-licensorslicensorIdmodeleditparamsbycategory)  | Получение параметров для категории по hid |
| [GET /licensors/[licensorId]/modelEdit/params/byModel](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/params#get-licensorslicensorIdmodeleditparamsbymodel)  | Получение параметров модели по modelId со значениями из репорта |
| [POST /licensors/[licensorId]/modelEdit/requests](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/requests#post-licensorslicensorIdmodeleditrequests)  | Создание заявки на создание/изменение модели |
| [GET /licensors/[licensorId]/modelEdit/requests](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/requests#get-licensorslicensorIdmodeleditrequests)  | Получение списка заявок на создание/изменение модели |
| [GET /licensors/[licensorId]/modelEdit/requests/[requestId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/requests/%5BrequestId%5D#get-licensorslicensorIdmodeleditrequestsrequestid)  | Получение заявки на создание/изменение модели |
| [PUT /licensors/[licensorId]/modelEdit/requests/[requestId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/requests/%5BrequestId%5D#put-licensorslicensorIdmodeleditrequestsrequestid)  | Изменение заявки на создание/изменение модели |
| [DELETE /licensors/[licensorId]/modelEdit/requests/[requestId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/requests/%5BrequestId%5D#delete-licensorslicensorIdmodeleditrequestsrequestid)  | Удаление заявки на создание/изменение модели |
| [GET /licensors/[licensorId]/modelEdit/requests/[requestId]/comments](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/requests/%5BrequestId%5D/comments#get-licensorslicensorIdmodeleditrequestsrequestidcomments)  | Получение комментариев к заявке на создание/изменение модели |
| [GET /licensors/[licensorId]/modelEdit/params/colors](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/params/colors#get-licensorslicensorIdmodeleditparamscolors)  | Получение вендорских цветов |
| [GET /licensors/[licensorId]/modelEdit/params/colors/[colorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/params/colors/%5BcolorId%5D#get-licensorslicensorIdmodeleditparamscolorscolorid)  | Получение вендорского цвета по его идентификатору |
| [POST /licensors/[licensorId]/modelEdit/params/colors](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/params/colors#post-licensorslicensorIdmodeleditparamscolors)  | Создание вендорского цвета |
| [PUT /licensors/[licensorId]/modelEdit/params/colors/[colorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/params/colors/%5BcolorId%5D#put-licensorslicensorIdmodeleditparamscolorscolorid)  | Изменение существующего вендорского цвета |
| [DELETE /licensors/[licensorId]/modelEdit/params/colors/[colorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/params/colors/%5BcolorId%5D#delete-licensorslicensorIdmodeleditparamscolorscolorid)  | Удаление существующего вендорского цвета |
| [GET /licensors/[licensorId]/modelEdit/params/sku](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/params/sku#get-licensorslicensorIdmodeleditparamssku)  | Получение списка SKU модели |
| [GET /licensors/[licensorId]/modelEdit/params/sku/[skuId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/params/sku/%5BskuId%5D#get-licensorslicensorIdmodeleditparamsskuskuid)  | Получение SKU модели по его идентификатору |
| [POST /licensors/[licensorId]/modelEdit/params/sku](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/params/sku#post-licensorslicensorIdmodeleditparamssku)  | Создание нового SKU модели |
| [PUT /licensors/[licensorId]/modelEdit/params/sku/[skuId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/params/sku/%5BskuId%5D#put-licensorslicensorIdmodeleditparamsskuskuid)  | Изменение существующего SKU модели |
| [DELETE /licensors/[licensorId]/modelEdit/params/sku/[skuId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/modelEdit/params/sku/%5BskuId%5D#delete-licensorslicensorIdmodeleditparamsskuskuid)  | Удаление существующего SKU модели |
| [PUT /vendors/[vendorId]/[productKey]/balance/clientLogins](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/%5BproductKey%5D/balance/clientLogins#put-vendorsvendoridproductkeybalanceclientlogins)  | Связывание пользователей с клиентом в балансе |
| [POST /vendors/[vendorId]/[productKey]/billing/requestPayment](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/%5BproductKey%5D/billing/requestPayment#post-vendorsvendoridproductkeybillingrequestPayment)  | Формирование недовыставленного счета |
| [GET /vendors/[vendorId]/[productKey]/billing/availableTransfer](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/%5BproductKey%5D/billing/availableTransfer#get-vendorsvendoridproductkeybillingavailabletransfer)  | Запрос суммы, доступной для перевода средств между офертными кампаниями вендора или агенства |
| [POST /vendors/[vendorId]/[productKey]/billing/makeTransfer/[toVendorId]/[toProductKey]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/%5BproductKey%5D/billing/makeTransfer#post-vendorsvendoridproductkeybillingmaketransfertovendoridtoproductkey)  | Перевод средств между офертными кампаниями вендора или агенства |
| [POST /vendors/[vendorId]/offer/accept](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/offer#post-vendorsvendoridofferaccept)  | Принятие оферты существующим вендором, работающим по контракту |
| [POST /files/[serviceKey]/upload/multipart](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/files/[serviceKey]/upload#post-filesdocumentsuploadmultipart) | Загрузка файла документооборота оферты с компьютера |
| [POST /files/[serviceKey]/upload/url](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/files/[serviceKey]/upload#post-filesdocumentsuploadurl) | Загрузка файла документооборота оферты по URL-адресу |
| [GET /files/[serviceKey]/meta/{id}](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/files/[serviceKey]/meta#get-filesdocumentsmetaid) | Получение мета-данных загруженного файла |
| [GET /vendors/[vendorId]/reports/stats](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/reports/stats#get-vendorsvendoridreportsstats) | Получение отчётов |
| [GET /vendors/[vendorId]/categories/top](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/categories#get-vendorsvendoridcategoriestop) | Получение самой популярной категории вендора |
| [GET /oauth/contentApi/link](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/oauth#get-oauthcontentApilink) | Запрос ссылки для получения oauth-токена для текущего пользователя |
| [GET /vendors/[vendorId]/opinions](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/opinions#get-vendorsvendoridopinions) | Получение отзывов на товары вендора по его vendorId |
| [GET /vendors/[vendorId]/opinions/count](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/opinions#get-vendorsvendoridopinionscount) | Получение количества отзывов на товары вендора по его vendorId |
| [POST /vendors/[vendorId]/opinions/[opinionId]/comment](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/opinions#post-vendorsvendoridopinionsopinionidcomment) | Создание комментария к отзыву или комментарию на отзыв |
| [PUT /vendors/[vendorId]/opinions/[opinionId]/comment/[commentId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/opinions#put-vendorsvendoridopinionsopinionidcommentcommentid) | Изменение комментария к отзыву или комментарию на отзыв |
| [DELETE /vendors/[vendorId]/opinions/[opinionId]/comment/[commentId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/opinions#delete-vendorsvendoridopinionsopinionidcommentcommentid) | Удаление комментария к отзыву или комментарию на отзыв |
| [GET /vendors/[vendorId]/questions](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/questions)|Получение вопросов на товары вендора по его vendorId|
| [POST /vendors/[vendorId]/questions/[questionsId]/answer](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/questions)|Создание ответа на вопрос по модели|
| [PUT /vendors/[vendorId]/questions/[questionsId]/answer/[answerId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/questions)|Изменение ответа на вопрос по модели|
| [DELETE /vendors/[vendorId]/questions/[questionsId]/answer/[answerId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/questions)|Удаление ответа на вопрос по модели|
| [POST /vendors/[vendorId]/questions/[questionId]/answer/[answerId]/comment](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/questions)|Создание комментария к ответу на вопрос по модели|
| [PUT /vendors/[vendorId]/questions/[questionId]/answer/[answerId]/comment/[commentId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/questions)|Изменение комментария к ответу на вопрос по модели|
| [DELETE /vendors/[vendorId]/questions/[questionId]/answer/[answerId]/comment/[commentId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/questions)|Удаление комментария к ответу на вопрос по модели|
| [GET /vendors/[vendorId]/manager](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/manager#get-vendorsvendoridmanager) | Получение данных менеджера, назначенного вендору |
| [PUT /vendors/[vendorId]/manager](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/manager#put-vendorsvendoridmanager) | Назначение менеджера карточке вендора |
| [GET /overrideClones](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/overrideClones#get-overrideClones) | Зачитывание всех клонов магазинов, переопределенных на стороне Кабинета Вендора |
| [PUT /overrideClones](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/overrideClones#put-overrideClones) | Устанавливает клоны магазинов, переопределяя региональные в Кабинете Вендора или формируя новые группы |
| [GET /vendors/[vendorId]/manager](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/manager#get-vendorsvendoridmanager) | Возвращает данные менеджера для указанного вендора |
| [PUT /vendors/[vendorId]/manager](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/manager#put-vendorsvendoridmanager) | Устанавливает менеджера для указанного вендора |
| [DELETE /vendors/[vendorId]/manager](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/manager#delete-vendorsvendoridmanager) | Удаляет менеджера у указанного вендора (передаёт поддержке) |
| [POST /vendors/[vendorId]/brandzone](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/brandzone#post-vendorsvendoridbrandzone) | Добавление услуги "Бренд-зона на Сервисе Яндекс.Маркет" вендору по его vendorId |
| [PUT /vendors/[vendorId]/brandzone](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/brandzone#put-vendorsvendoridbrandzone) | Изменение информации об услуге "Бренд-зона на Сервисе Яндекс.Маркет" вендора по его vendorId |
| [GET /vendors/[vendorId]/brandzone](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/brandzone#get-vendorsvendoridbrandzone) | Получение информации об услуге "Бренд-зона на Сервисе Яндекс.Маркет" вендора по его vendorId |
| [GET /vendors/[vendorId]/brandzone/tariffs](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/brandzone/tariffs#get-vendorsvendoridbrandzonetariffs) | Получение текущего тарифа услуги "Бренд-зона на Сервисе Яндекс.Маркет" для вендора |
| [POST /vendors/[vendorId]/brandzone/tariffs](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/brandzone/tariffs#post-vendorsvendoridbrandzonetariffs) | Добавление/изменение следующего тарифа услуги "Бренд-зона на Сервисе Яндекс.Маркет" для вендора |
| [PUT /vendors/[vendorId]/brandzone/placement](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/brandzone/placement#put-vendorsvendoridbrandzoneplacement) | Включение/выключение услуги "Бренд-зона на Сервисе Яндекс.Маркет" для вендора |
| [GET /vendors/[vendorId]/content/models](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/content) | Получение списка товаров и заявок на модели вендора |
| [GET /vendors/[vendorId]/content/models/count](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/content) | Получение числа товаров (моделей + SKU) вендора |
| [GET /vendors/[vendorId]/content/requests/count](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/content) | Получение числа заявок на редактироваеме моделей по состояниям |
| [GET /vendors/[vendorId]/content/categories](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/content) | Получение иерархии категорий вендора |
| [GET /vendors/[vendorId]/content/categories/[categoryId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/content) | Получение информации о категории вендора по её идентификатору |
| [GET /licensors](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors#get-licensors)  | Зачитывание списка карточек лицензиаров |
| [POST /licensors](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors#post-licensors)  | Создание новой карточки лицензиара |
| [GET /licensors/[licensorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D#get-licensorslicensorid)  | Зачитывание карточки лицензиара |
| [PUT /licensors/[licensorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D#put-licensorslicensorid)  | Редактирование карточки лицензиара |
| [POST /licensors/[licensorId]/offer/accept](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/offer#post-licensorslicensorofferaccept)  | Принятие оферты лицензиаром |
| [GET /licensors/[licensorId]/manager](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/manager#get-licensorslicensorIdmanager) | Получение данных менеджера, назначенного лицензиару |
| [PUT /licensors/[licensorId]/manager](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/manager#put-licensorslicensorIdmanager) | Назначение менеджера карточке лицензиара |
| [DELETE /licensors/[licensorId]/manager](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/manager#delete-licensorslicensorIdmanager) | Удаление менеджера у карточки лицензиара (передача карточки в саппорт) |
| [GET /licensors/[licensorId]/role/[role]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/role#get-licensorslicensorIdrolerole) | Возвращает список пользователей, обладающих указанной ролью для заданного лицензиара |
| [PUT /licensors/[licensorId]/role/[role]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/role#put-licensorslicensorIdrolerole) | Устанавливает список пользователей, обладающих указанной ролью для заданного лицензиара |
| [GET /licensors/suggest/[entity]/name](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors#get-licensorssuggestentityname) | Получение списка подходящих имен для лицензиара, франшизы или персонажа (саджест)|
| [GET /licensors/[licensorId]/constraints](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/constraints#get-licensorslicensorIdconstraints) | Возвращает список ограничений на маркетные бренды и категории, установленные для заданного лицензиара |
| [POST /licensors/[licensorId]/constraints/[brandId]/[categoryId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/constraints#post-licensorslicensorIdconstraintsbrandIdcategoryId) | Устанавливает одно ограничение на маркетный бренд и категорию для заданного лицензиара |
| [DELETE /licensors/[licensorId]/constraints/[brandId]/[categoryId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D/constraints#delete-licensorslicensorIdconstraintsbrandIdcategoryId) | Удаляет одно ограничение на маркетный бренд и категорию для заданного лицензиара |
