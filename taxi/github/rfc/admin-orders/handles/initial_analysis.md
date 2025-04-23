# Админка заказов: анализ ручек

## Общие пожелания

- нужно подумать о том, чтобы отказаться от всего, что связано с db.cities, если это возможно

## Не для MVP, есть YAML


### /api/orders/

**Код**: `taxiadmin.api.views.orders.get_orders`

**ТЗ нa фичу**: центральная ручка, отдельного ТЗ нет.

**Дашборды**:
https://grafana.yandex-team.ru/d/zVB75dkWk/taxi_conductor_taxi_admin#ymsh-admin_mobile_yandex-team_ru_api_orders

**TODO:** Проверить YAML на сооответствие реальным параметрам запроса и ответа

#### Декораторы и хелперы

- `decorators.perm_required` - см. в разделе "Типовые решения"
- `apiutils.log_request` - см. в разделе "Типовые решения"
- `apiutils.json_request` - см. в разделе "Типовые решения"
- `apiutils.json_response` - см. в разделе "Типовые решения"
- `apiutils.field_permissions_required` - см. в разделе "Типовые решения"
- `apiutils.json_validator` - см. в разделе "Типовые решения"
- `apiutils.localized_view` - см. в разделе "Типовые решения"

- `request.time_storage.get_timer` - ?

#### Зависимости

- `orders._get_search_filters` - формирование списка фильтров поиска

- `audit.log_action` - на всю ручку: через api-admin (описать в yaml)
    
    если же нужно отдельные куски кода или по определённому условию,
    то надо дорабатывать АБК либо ходить в нужно API
    (~~а его отдельного нет, оно только в api-admin живёт~~) есть сервис и клиент

- `orders._clean_city_id` - поддержка переводов названий городов

- `country_manager.clean_international_phone`
    1) подключить `client_territories: yes` в `service.yaml`
    2) `from taxi.util import cleaners`
    3) `phone_value = await cleaners.clean_international_phone(context.client_territories, phone, force=True)`

- `common.get_phone_objects_with_permission` - проверка доступа к удалённым телефонам
    прокидывать запрос на удалённые телефоны из АБК (?) + пермишн (есть/нет)
    тут главное не отдавать по одному урлу разные данные внезапно
    (можно добавить фильтр в эксперименты, чтобы в ручку присылать
    `deleted_phones: true` если у юзера есть пермишн на это)

- `adminutil.validate_order_query_dates` - валидация дат в фильтре поиска
    (используется только тут, скопировать код в локальные хелперы)

- `config.ORDERS_ACCESS_BY_COUNTRY` - доп. ограничения по странам
    (вынести проверку `countries_filter` из ручки в хелперы)

- `orders._restrict_filter_by_permissions` (доп. ограничения по пермишнам)

- `admin_restrictions.check_restrictions` - посмотреть
    `experiments_filters: true` в **api-admin** (`service_schemes`)

- `yt_admin.get_orders_page` - получение списка заказов (нужно переносить в py3)
    также нужно будет переносить в py3 subcallees
    (попробовать добавить в `archive_api` ?)
    (проблема в поиске свежих заказов по параметрам, archive-api ищет только по `ids`)
    (заказать поиск по параметрам заказа в order-core, а пока ходить в базу)

- `userapi.get_user_phones` - получение номеров телефонов (не нужно, т.к. больше не отдаём это в заказе)
    (сейчас берётся прямо из базы, нужно как тут
    https://wiki.yandex-team.ru/taxi/backend/architecture/user-api/#ispolzovanijatelefonov)
    1) `client_user_api: yes` в `service.yaml`
    2) см. `context.client_user_api.get_user_phone_bulk`

- `common.get_all_parks_and_real` - получение списка парков (may be deprecated?)
    посмотреть задачу про выпиливание `real_clids`
    (это https://st.yandex-team.ru/TAXIACCESSDATA-357)
    
    а за именами парков ходить в ручку 
    https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Uservices/parks-commute/api/api/#v1parksretrieve_by_clid

- `taxi_helpers.get_categories_translations` - переводы тарифных категорий
    см. https://wiki.yandex-team.ru/taxi/backend/automatization/CodegenPy3Users/#9.translations

- `city_manager.localized_city_name` - посмотреть работу с локализациями
    (`translations.translations.geoareas.get_string_or_default`)
    ~~(тут придётся ходить в `db.cities` за ключом для танкера в поле `eng`)~~
    ~~(либо написать что-то обратное `_translate_city_id`, чтобы не ходить в `db.cities`)~~
    в итоге используются переводы из ручки tariff_zones сервиса тарифов
    

- `translations.translations.tariff.get_string_or_default` - переводы валюты
    (строки и символы)
    **РЕШЕНИЕ:** нужно добавить в `service.yaml`:
    ```
    translations:
     - tariff
    ```
    usage: `context.translations.tariff.get_string_or_default`,

- `orders._translate_tariff_class` - перевод тарифа
    (берётся из `taxi_helpers.get_categories_translations`)


#### Осталось сделать

- [x] проверить работу ручки в анстейбле (без ограничений, аудита и фильтров, только получение данных из архива и базы)
- [x] проверить работу ручки в тестинге (без ограничений, аудита и фильтров, только получение данных из архива и базы)
- [x] разобраться, почему py3 не отдаёт некоторые заказы, которые есть в py2
- [x] добавить кэширование зон из сервиса tariffs
- [x] проверить работу ручки в анстейбле (без ограничений и аудита, проверка фильтров)
- [x] проверить работу ручки в тестинге (без ограничений и аудита, проверка фильтров)
- [x] добавить `{"dst": "tariffs","src": "admin-orders"}` в TVM_RULES (unstable & tst done)
- [x] добавить перевод названия города из запроса (позже)
- [x] подключить client_audit и логировать запросы самостоятельно
- [x] добавить ограничение доступа по странам (задал вопрос как лучше)
- [x] добавить `{"dst": "audit","src": "admin-orders"}` в TVM_RULES (unstable & tst done)
- [x] проверить audit логи в тестинге (нужно выкатить schemas и py3)
- [x] настроить АБК (прописать ручку в `service_schemas` и подёргать её)
- [x] добавить эксперимент для просмотра удалённых пользователей (?)
    эксперимент не даёт отправлять поля в query, только в body (?)
    (UPD: эта фича не нужна совсем) 
- [x] добавить эксперимент для поддержки admin_restrictions
    (просто продублировать секцию /orders/ в секцию /admin/admin-orders/v1/orders/)
    (testing: done)
- [x] добавить правило эксперимента `admin_restrictions` для пермишна `view_orders_limited`,
    секция `/admin/admin-orders/v1/orders/`
    (замена конфигов `ORDERS_HISTORY_VIEW_LIMIT_RESULTS` и `ORDERS_HISTORY_VIEW_LIMIT_DAYS`)
    (уже неактуально, от этого пермишна отказались)
- [x] замержить пул-реквест в schemas для parks-replica
- [x] замержить пул-реквест в backend-py3 для parks-replica
- [x] сделать rebase от текущего develop в py3 (отдельной веткой)
- [x] подключить кодогенерированный клиент для parks-replica и добавить имя парка из сервиса parks-replica
- [x] добавить `{"dst": "parks-replica", "src": "admin-orders"}` в TVM_RULES (unstable & tst done)
- [ ] проверить работу admin_restrictions в тестинге (после того, как фронты перенесут ручку)
- [x] проверить, насколько нужен пермишн `search_by_user_phone` и `search_by_driver_license`

- [ ] тесты на даты (проверка validate_order_query_dates)
- [x] тесты на телефоны
- [x] тесты на телефоны удалённые
- [x] тесты на города
- [x] тесты на страны
- [ ] тесты на фильтры (м.б. тестить саму функцию фильтров, а не всю ручку)

- [ ] добавить `{"dst": "tariffs","src": "admin-orders"}` в TVM_RULES (production)
- [ ] добавить `{"dst": "audit","src": "admin-orders"}` в TVM_RULES (production)
- [ ] добавить `{"dst": "territories","src": "admin-orders"}` в TVM_RULES (production)
- [ ] добавить `{"dst": "user-api","src": "admin-orders"}` в TVM_RULES (production)
- [ ] добавить `{"dst": "parks-replica", "src": "admin-orders"}` в TVM_RULES (production)
- [ ] добавить эксперимент для поддержки admin_restrictions (production)
    (просто продублировать секцию /orders/ в секцию /admin/admin-orders/v1/orders/)

- [x] выпилить translations.geoareas из service.yaml (не используется)
- [x] выпилить ненужные конфиги из service.yaml и из схем конфигов
    (например ALL_CATEGORIES_IN_ADMIN по факту не нужен)

#### Внешние сервисы (TODO)

#### Используемые конфиги (TODO)

- `ORDERS_ACCESS_BY_COUNTRY` - не будем использовать, т.к. это был конфиг на включение фичи
    (если нужно будет сотруднику дать возможность увидеть заказы не только из его страны,
    нужно это делать через его персональные или групповые доступы)
- `ORDERS_HISTORY_VIEW_LIMIT_DAYS` - больше не нужен, т.к. будет определяться в эксперименте admin_restrictions
- `ORDERS_HISTORY_VIEW_LIMIT_RESULTS` - больше не нужен, т.к. будет определяться в эксперименте admin_restrictions

#### Используемые коллекции (TODO)

- `cities` (не используем, вместо этого ходим в сервис `tariffs`)
- `tariff_settings` (не используем, вместо этого ходим в сервис `tariffs`)
- `parks` (не используем, вместо этого ходим в сервис `parks-replica`)

#### Тесты

- `test_taxiadmin_api_views_orders.test_get_deleted_users_orders`
- `test_taxiadmin_api_views_orders.test_get_orders`
- `test_taxiadmin_api_views_orders.test_get_orders_city_error`
- `test_taxiadmin_api_views_orders.test_get_orders_pd_access`
- `test_taxiadmin_api_views_orders.test_get_orders_by_countries` (by URL)

#### Вопросы для прояснения

- **ВОПРОС:** можно ли в ответе возвращать `payment_type` пустой строкой вместо `null`?
    или вообще не возвращать, например?
    иначе непонятно как описать схему, которая требует только один тип
    либо заменять `\n(\s+)type:\n(\s+)- string\n(\s+)- 'null'`
    на `\n$1oneOf:\n$2- type: string\n$3- type: 'null'`
    
    **ОТВЕТ:** можно не возвращать поле, оно не покажется,
    так же как если бы пришло `null` в значении

- `field_permissions_required` - будет доработка в дин.пермишнах в АБК

- пермишны из перечисленных в схеме ручки нужно прокидывать из api-admin в запросе (?),
    чтобы дополнительно фильтровать отдаваемые данные
    (использовать эксперимент с `admin_restrictions` (?))

- как ускорить ручку, если в ней будет столько походов в различные сервисы и базы?
    как вариант, рассмотреть `asyncio.gather`
    (можно вторым этапом после снятия таймингов)
    (также кэшируем ответы сервисов через `memcache.memoize`)
    (нужно будет доработать, чтобы при падении сервисов использовать старый кэш,
    сейчас memcache его инвалидирует и мы остаёмся без данных (?))

- **ВОПРОС**: чем заменять `request.time_storage.get_timer`
  **ОТВЕТ**: см. `performance.time_context` из `taxi.util.performance`

#### Список подзадач для реализации

- [x] реализовать отдачу данных без ограничений, чтобы формат старой и новой ручки был одинаковый
- [ ] реализовать аналог `field_permissions_required` (будет сделано в дин. пермишнах)
- [ ] добавить эксперименты 'admin_restrictions' для пробрасывания пермишнов
- [ ] проверить в тестовой админке, что отсутствие полей аналогично `null`
- [ ] приготовить список тест-кейсов
- [x] заменить `localized_city_name`, чтобы не ходить в `db.cities` (если не сложно)
 

### /api/order/<_id>/attach_voucher/

**ВАЖНО!** Ручку планируется не переносить, а отдать в сервис svo (когда будет).

**Код**: `taxiadmin.api.views.orders.attach_voucher`

**ТЗ нa фичу**: https://st.yandex-team.ru/TAXIBACKEND-18974

**Дашборды**: отсутствуют.

**TODO:** Проверить YAML на сооответствие реальным параметрам запроса и ответа

#### Декораторы и хелперы

- `csrf.csrf_exempt` - ?
- `decorators.perm_required` - `py3.taxi.util.perm_required` (**проверить**)
- `apiutils.json_request` - не требует переноса в py3
- `apiutils.json_response` - не требует переноса в py3
- `apiutils.json_validator` - мигрирует в YAML-схему
- `audit.log_action_with_ticket` (и `audit.log_action`) - переносить в py3 (?) в external или util
- `async.inline_callbacks` - не требует переноса в py3

#### Зависимости

- `orders.attach_voucher_to_order`
- `taxi.internal.archive.get_order_proc_by_id`
- `taxi.external.archive.get_order_proc_by_id`
- `orders.get_voucher_by_code_and_date`
- `orders.get_voucher_from_archive`
- `orders.archive_voucher_to_doc`
- `orders.get_rows_from_archive`
- `orders._build_archive_voucher_query`
- `taxi.internal.replication.get_table_path`
- `taxi.external.yt_wrapper.get_yt_replication_runtime_clients`
- `taxi.internal.archive.perform_select_rows`
- `taxi.external.archive.perform_select_rows`
- `orders.find_order_proc_id_by_voucher_id`
- `orders._build_archive_order_proc_query`
- `taxi.internal.archive.get_order_by_exact_id`
- `taxi.internal.archive.restore_order`
- `taxi.internal.order_kit.invoice_handler.close_with_voucher`
    (!!!) вызывается также из обычного завершения поездки (надо думать, как это выдрать)
- `taxi_stq.stq_client.order_billing`
- `orders.attach_voucher_to_order_proc`
- `taxi.internal.archive.restore_order_proc`

#### Внешние сервисы (TODO)

#### Используемые конфиги

- `ADMIN_USE_ARCHIVE_API`
- `YT_REPLICATION_RUNTIME_CLUSTERS`
- `ARCHIVE_API_YT_RUNTIME_REPLICATION_DELAY`
- ??? просмотреть ещё раз

#### Тесты

- `test_taxiadmin_api_views_orders.test_attach_voucher`


## Не для MVP, нет YAML


### /api/order/<_id>/ (TODO)

**Код**: `taxiadmin.api.views.orders.get_order`

**ТЗ нa фичу**: отдельного ТЗ нет.

**Дашборды**: 

**TODO**: 

#### Декораторы и хелперы

- `csrf.csrf_exempt` - ? (проверить)
- `decorators.perm_required` - `py3.taxi.util.perm_required` (**проверить**)
- `apiutils.log_request` - см. `x-taxi-middlewares:` в YAML и `codegen`
- `apiutils.json_request` - не требует переноса в py3
- `apiutils.json_response` - не требует переноса в py3
- `apiutils.json_validator` - мигрирует в YAML-схему
- `apiutils.localized_view` - ? (возможно, нужен перенос в py3)

- `request.time_storage.get_timer`

#### Зависимости (TODO)

- ``

#### Внешние сервисы (TODO)

#### Используемые конфиги (TODO)

- `ADMIN_USE_ARCHIVE_API`
- `ORDERS_ACCESS_BY_COUNTRY`
- `ENABLE_DRIVER_CHANGE_COST`
- `EDITABLE_REQUIREMENTS_BY_ZONE`
- TODO: see callees

#### Тесты (TODO)

- ``


## Подходят для MVP


### /api/order/<_id>/restore/

**Код**: `taxiadmin.api.views.orders.restore_order`

**ТЗ нa фичу**: TODO: собрать список задач, найти на вики описание (если есть).

**Дашборды**:
https://grafana.yandex-team.ru/d/zVB75dkWk/taxi_conductor_taxi_admin#ymsh-admin_mobile_yandex-team_ru_api_order_order_id_restore

**TODO:**
- ~~доработка taxi.clients.archive_api~~ прописать по схеме (см. примеры) 
- добавление тестов
- добавление файла для ручек в АБК

#### Декораторы и хелперы

- `csrf.csrf_exempt` - не требуется
- `decorators.perm_required` - см. в разделе "Типовые решения"
- `apiutils.log_request` - см. в разделе "Типовые решения"
- `apiutils.json_request` - см. в разделе "Типовые решения"
- `apiutils.json_response` - см. в разделе "Типовые решения"
- `apiutils.json_validator` - мигрирует в YAML-схему

#### Зависимости

- `taxi.internal.archive.restore_order`
- `taxi.external.archive.restore_order`
- `taxi.internal.archive.restore_order_proc`
- `taxi.external.archive.restore_order_proc`

Для использования этих зависимостей в py3 нужно будет ~~добавить функции 
восстановления заказа и прока в taxi.clients.archive_api~~ ходить в ручки
сервиса archive-api, описав их в конфиге клиента.

#### Внешние сервисы (TODO)

- archive-api (есть поддержка в py3, но нужно добавление новых функций там)

#### Используемые конфиги

Только те, которые используются самим сервисом archive-api, тут они не нужны.

#### Тесты

Отсутствуют.


### /api/order/<_id>/cancel/user/

**Код**: `taxiadmin.api.views.orders.cancel_by_user`

**ТЗ нa фичу**: отдельного ТЗ нет.

**Дашборды**: 

**TODO**: 
- (в целом) прописать формат ответа 4xx ошибок (стандартный, для АБК)

#### Декораторы и хелперы

- `csrf.csrf_exempt` - ?
- `decorators.perm_required` - АБК (**проверить**)
- `apiutils.json_request` - не требует переноса в py3
- `apiutils.json_response` - не требует переноса в py3
- `apiutils.json_validator` - мигрирует в YAML-схему
- `apiutils.localized_view` - ? (возможно, нужен перенос в py3)

- `audit_actions.cancel_order_by_user` - АБК (?)
- `admin_permissions.manage_order` - АБК (?)
- `apiutils.error_http_response` - АБК
- `audit.log_action` - АБК

#### Зависимости

- `event_handler.cancel_by_user` - используется только этой ручкой
    (но скорее всего, будем дергать `/v1/tc/order-cancel` из order-core,
     после [небольших доработок](https://st.yandex-team.ru/TAXIARCHREVIEW-82#5e2020ca4b38e12d025a894a))
- (TODO: дописать зависимости, если переносим код, а не ходим в order-core)

#### Внешние сервисы (TODO)

- order-core (?)

#### Используемые конфиги (TODO)

- ``

#### Тесты (TODO)

- ``


### /api/order/<_id>/cancel/park/

**Код**: `taxiadmin.api.views.orders.cancel_by_park`

**ТЗ нa фичу**: отдельного ТЗ нет.

**Дашборды**: 

**TODO**: 

#### Декораторы и хелперы

- `csrf.csrf_exempt` - ?
- `decorators.perm_required` - АБК (**проверить**)
- `apiutils.json_request` - не требует переноса в py3
- `apiutils.json_response` - не требует переноса в py3
- `apiutils.json_validator` - мигрирует в YAML-схему
- `apiutils.localized_view` - ? (возможно, нужен перенос в py3)

- `admin_permissions.manage_order` - АБК (?)
- `permissions.authorize_request` - АБК (?)
- `audit_actions.cancel_order_by_park` - АБК (?)
- `apiutils.error_http_response` - АБК
- `audit.log_action` - АБК

#### Зависимости

- `dbh.order_proc.Doc.update_taxi_status` - заменить на поход в order-core (?)

#### Внешние сервисы (TODO)

- ``

#### Используемые конфиги (TODO)

- ``

#### Тесты (TODO)

- ``


### /api/order/<_id>/autoreorder/

**Код**: `taxiadmin.api.views.orders.autoreorder`

**ТЗ нa фичу**: отдельного ТЗ нет.

**Дашборды**: 

**TODO**:
- решить, как обрабатывать NotAcceptable (сейчас 500-ит)

#### Декораторы и хелперы (TODO)

- `csrf.csrf_exempt` - ?
- `decorators.perm_required` - АБК (**проверить**)
- `apiutils.json_request` - не требует переноса в py3
- `apiutils.json_response` - не требует переноса в py3
- `apiutils.json_validator` - мигрирует в YAML-схему
- `apiutils.localized_view` - ? (возможно, нужен перенос в py3)

- `admin_permissions.manage_order` - АБК (?)
- `permissions.authorize_request` - АБК (?)
- `audit_actions.autoreorder` - АБК (?)
- `apiutils.error_http_response` - АБК
- `audit.log_action` - АБК

#### Зависимости (TODO)

- `event_handler.autoreorder` - используется только этой ручкой
- (TODO: дописать зависимости)

#### Внешние сервисы (TODO)

- ``

#### Используемые конфиги (TODO)

- ``

#### Тесты (TODO)

- ``


### /api/order/<_id>/report/retry/

**Код**: `taxiadmin.api.views.orders.retry_report`

**ТЗ нa фичу**: отдельного ТЗ нет.

**Дашборды**: 

**TODO**: Подходит для MVP, т.к. есть интеграция с сервисами, stq
Минус: нужно решить, что делать с походом в `db.order_reports_sent`.

#### Декораторы и хелперы (TODO)

- `csrf.csrf_exempt` - ?
- `decorators.perm_required` - АБК (**проверить**)
- `apiutils.log_request` - см. `x-taxi-middlewares:` в YAML и `codegen`
- `apiutils.json_request` - не требует переноса в py3
- `apiutils.json_response` - не требует переноса в py3
- `apiutils.json_validator` - мигрирует в YAML-схему
- `apiutils.localized_view` - ? (возможно, нужен перенос в py3)

- `admin_permissions.manage_order` - АБК (?)
- `audit_actions.retry_report` - АБК (?)
- `apiutils.error_http_response` - АБК
- `apiutils.not_found_response` - АБК
- `audit.log_action` - АБК

#### Зависимости (TODO)

- `archive.get_order_proc_by_id` - поход в archive-api
- `db.order_reports_sent.find_and_modify` - ?
- `email_manager.get_email` - заменить на поход в admin-personal (`/user/{id}/retrieve`)
- `ride_report.send_report_task.call` - используется также в status_handling
- (TODO: дописать зависимости)

#### Внешние сервисы и компоненты

- admin-personal
- archive-api
- stq

#### Используемые конфиги (TODO)

- `ADMIN_USE_ARCHIVE_API`
- ? (TODO: проверить в зависимостях)

#### Тесты (TODO)

- ``


## Ждут анализа


### /api/order/<_id>/switch_expired_back_to_card/

**Код**: `taxiadmin.api.views.orders.switch_expired_back_to_card`

**ТЗ нa фичу**: отдельного ТЗ нет.

**Дашборды**: 

**TODO**: 
- возможно, эту ручку нужно будет перенести в отдельный сервис admin-payments

#### Декораторы и хелперы (TODO)

- `csrf.csrf_exempt` - ?
- `decorators.perm_required` - АБК (**проверить**)
- `apiutils.json_request` - не требует переноса в py3
- `apiutils.json_response` - не требует переноса в py3
- `apiutils.json_validator` - мигрирует в YAML-схему
- `apiutils.localized_view` - ? (возможно, нужен перенос в py3)

- `admin_permissions.manage_order` - АБК (?)
- `audit_actions.switch_expired_back_to_card` - АБК (?)
- `apiutils.error_http_response` - АБК
- `audit.log_action` - АБК

#### Зависимости (TODO)

- `invoice_handler.switch_expired_back_to_card` - используется только этой ручкой
- (TODO: дописать зависимости)

#### Внешние сервисы (TODO)

- ``

#### Используемые конфиги (TODO)

- ``

#### Тесты (TODO)

- ``

### /api/order/<_id>/update_transactions/

**Код**: `taxiadmin.api.views.orders.update_transactions`

**ТЗ нa фичу**: отдельного ТЗ нет.

**Дашборды**: 

**TODO**: 
- возможно, эту ручку нужно будет перенести в отдельный сервис admin-payments

#### Декораторы и хелперы

- `csrf.csrf_exempt` - ?
- `decorators.perm_required` - АБК (**проверить**)
- `apiutils.json_request` - не требует переноса в py3
- `apiutils.json_response` - не требует переноса в py3
- `apiutils.json_validator` - мигрирует в YAML-схему

- `admin_permissions.manage_order` - АБК (?)
- `apiutils.not_found_response` - АБК
- `audit.log_action` - АБК

- `audit_actions.update_transactions` - сейчас отсутствует (добавить в АБК и юзать?)

#### Зависимости (TODO)

- `dbh.orders.Doc._update`
- `dbh.orders.Doc.update_transactions_errors`
- `stq_client.update_transactions_call`
- (TODO: дописать зависимости)

#### Внешние сервисы (TODO)

- ``

#### Используемые конфиги (TODO)

- ``

#### Тесты (TODO)

- ``


## Типовые решения

### Декораторы

#### csrf.csrf_exempt

Можно не использовать, не работает в текущей реализации, т.к. вместо 
`django.middleware.csrf.CsrfViewMiddleware` используется кастомная проверка
CSRF-токена в `taxiadmin.middleware.BBAuthMiddleware` (если включен конфиг
`ADMIN_CSRF_VALIDATION_ENABLED`).

#### apiutils.field_permissions_required
Будет реализовано в АБК (TAXIPLATFORM-1931) примерно к 10.02.2020.
Настройка предполагается через dyn permissions.

#### decorators.perm_required
АБК (.yaml в папке `services_schemas`)
```
api:
  - path: v1/order/restore/
    methods:
      - method: post
        permissions:  # вот тут указать пермишны
          - restore_orders
```

#### apiutils.log_request
Включено по умолчанию. Если нужно задать кастомный `log_ident`, то нужно
задать его в секции `units.web` описания сервиса:
```yaml
units:
  web:
    log_ident: yandex-taxi-<service-name>-py3
```

Если нужно не логировать запрос или ответ (или этот декоратор отсутствует)
или изменить уровень логов, то нужно добавить секцию `x-taxi-middlewares`
(на уровне всего сервиса либо на уровне метода):
```yaml
x-taxi-middlewares:
  logging:
    level: warning
    log_request_body: false

paths:
  /ping:
    get:
      x-taxi-middlewares:
        tvm: no
        logging:
          level: info
          log_response_body: false
``` 

#### apiutils.json_request
Мигрирует в api.yaml сервиса в таком виде:
  ```yaml
  consumes:
    - application/json
  ```

#### apiutils.json_response
Мигрирует в api.yaml сервиса в таком виде:
  ```yaml
  produces:
    - application/json
  ``` 

#### apiutils.json_validator
Мигрирует в YAML-схему ручки.

#### apiutils.localized_view
Переделать на такое внутри ручки:
```
from taxi import locale
  
lang = locale.parse(request.accept_language, context.config)
```
(либо добавить на уровне запроса атрибут `lang` где-то в codegen (?))

### Тайминги

`request.time_storage.get_timer` - 

1)  импорты:
    ```
    from taxi.util import performance
    from taxi.util.aiohttp_kit import api as apiutils
    ```
2) обернуть ручку в `@apiutils.use_time_storage('<service>_<handle>')`
3) в аргументы ручки добавить `time_storage: performance.TimeStorage`
4) обернуть нужные куски кода так:
    ```
    with performance.time_context(time_storage, '<timer_name>'):
        do_stuff()
    ```

## TEMPLATE


### --- /TEMPLATE/HANDLE/URL/ ---

**Код**: `taxiadmin.api.views.orders.TEMPLATE_NAME`

**ТЗ нa фичу**: отдельного ТЗ нет.

**Дашборды**: 

**TODO**: 

#### Декораторы и хелперы (TODO)

- ``

#### Зависимости (TODO)

- ``

#### Внешние сервисы (TODO)

- ``

#### Используемые конфиги (TODO)

- ``

#### Тесты (TODO)

- ``
