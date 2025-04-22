# Перенос ручки couponactivate за passenger-authorizer

## Зачем

Уменьшить зависимость сервиса купонов от протокола, распил монолита.

## Какие сложности

Сейчас запросы в сервис купонов проксируются через клиентский протокол (aka монолит, backend-cpp). При проксировании в коде протокола собирается много дополнительной информации, которая достается из баз/конфигов/экспериментов. Из-за этого нельзя напрямую направить запросы в сервис купонов, нужно вынести соответствующую логику из протокола.

## Какая информация достается в коде протокола

### Пользователь

Используется экземпляр `models::User`, который получается из `user_doc`, взятого из базы по `user_id` из запроса. Используются поля:
- phone_id
- yandex_uid
- apns_token
- gcm_token
- device_id

Откуда можно взять:
- yandex_uid и phone_id приходят в хедерах от passenger-authorizer: [мануал](https://wiki.yandex-team.ru/taxi/backend/api-4.0/#httprequestheadersdljapasportnyxuid-ov)
- остальные данные можно взять из сервиса `user-api` (ручка `/users/get`).

#### bound_uids

Связанные `yandex_uid` (фониши, привязанные к порталу) будут приходить от passenger-authorizer.

### Настройки тарифа для зоны (`TariffSettings`)

Сейчас информация берется из базы `dbtaxi` (кэша).

Используются поля:
- zone_name
- country
- timezone
- payment_options
- categories

Откуда можно взять:
- Есть сервис `taxi-tariffs` (backend-py3) с ручкой выгрузки `tariff_settings` по списку зон.
- Над сервисом есть библиотека-кэш `taxi-tariffs` в uservices, ее и предлагается использовать, чтобы не создавать лишнюю нагрузку на сервис `taxi-tariffs`.

### Доступные в зоне категории

Вычисляются с использованием `tariff::VisibilityHelper`.

В настоящий момент в разработке библиотека `tariff-categories-visibility` в uservices, которая реализует функционал VisibilityHelper'а. Предлагается использовать эту библиотеку.

### Страна

Страна нужна для определения `region_id` (используется при походах в биллинг). Для работы со странами используется `models::CountryMap`.

Откуда можно взять:
- Есть сервис `taxi-territories` (backend-py3) с ручкой выгрузки информации по стране.

## Список всех полей с указанием источника

Ниже полный список полей, которые сейчас передаются во внутреннюю ручку `/v1/coupons/activate`:

request:
- user_id
- coupon
- zone_name
- selected_class
- payment_info (type, method_id)

passenger-authorizer:
- yandex_uids
- yandex_uid
- application
- locale
- user_ip
- phone_id

user-api (по user_id):
- apns_token
- gcm_token
- device_id

taxi-tariffs (по zone_name):
- country
- time_zone
- payment_options

taxi-territories (по country):
- region_id

tariff-categories-visibility (новая библиотека):
- zone_classes

deprecated:
- service_type: теперь определяется в коде сервиса купонов по конфигу на основе бренда

## Реализация

Есть два основных способа реализации логика сбора данных из источников:
- с помощью сервиса `api-proxy`
- вручную в коде сервиса купонов

Плюсы использования `api-proxy`:
- Не нужно писать код (boilerplate) -> изменения работают без перевыкаток.
- Не нужна новая ручка с другой схемой, `api-proxy` будет ходить в существующую ручку.
- Оптимальный обход источников в порядке топологической сортировки.
- Из коробки идет интеграция с сервисом статистики.

Минусы использования `api-proxy`:
- Дополнительная точка отказа. Допускаем, так как купоны не критичны для цикла заказа.

Предлагается обогащать данные из запроса в api-proxy походами в user-api и taxi-territores (с кэшом).
Остальная логика будет на стороне сервиса купонов с использованием библиотек для работы с тарифами и категориями.

## Как будет переключаться траффик

- В api-proxy будет заведена ручка со схемой, аналогичной `/3.0/couponactivate`
- Когда ручка будет готова, ее нужно будет прописать в роутинге passenger-authorizer'а в [конфиге](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/PASS_AUTH_ROUTER_RULES_2?name=PASS_AUTH_ROUTER_RULES_2).
- Затем переключить траффик на балансере через ПР в репозиторий [protocol-proxy](https://github.yandex-team.ru/taxi/protocol-proxy).
