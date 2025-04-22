# Проработка распиливания launch на микросервисы

## Полный ответ launch
```json
{
  "info": [],
  "order_for_another_init_distance_meters": 1,
  "server_time": "2019-12-13T11:08:11+0000",
  "show_me_min_distance": 1,
  "show_sms_menu_settings": false,
  "use_new_smooth_movement": false,
  "version_info": {
    "current_version": "3.63.0.0000",
    "update_notification_interval": 604800
  },
  "surge_notify": {},
  "client_geo_params": {},

  "authorized": true,
  "id": "",
  "loyal": true,
  "phones": {},
  "uuid": "",
  "phone": "",
  "token_valid": true,
  "name": "",
  "yandex_staff": true,

  "user_settings_hash": "",
  
  "experiments": [],
  "typed_experiments": {},
  
  "blocked": {},

  "payment_statuses_filter": [],

  "can_generate_referrals": false,

  "chat": {},

  "geofences_tag": "",

  "brandings": [],

  "parameters": {},

  "need_acceptance": [],

  "orders_state": {},
  "orders": [],

  "ask_feedback": {},

  "passenger_profile": {}
}

```

## Поля в launch / Микросервисы

### api-proxy

Поля, которые можно забрать из конфигов и экспериментов
подставит api-proxy

#### Запрос
Запрос от клиента.

#### Ответ
```json
{
  "info": [],
  "order_for_another_init_distance_meters": 1,
  "server_time": "2019-12-13T11:08:11+0000",
  "show_me_min_distance": 1,
  "show_sms_menu_settings": false,
  "use_new_smooth_movement": false,
  "version_info": {
    "current_version": "3.63.0.0000",
    "update_notification_interval": 604800
  },
  "surge_notify": {},
  "client_geo_params": {}
}
```

#### Fallback policy
Чтение констант из конфигов и экспериментов.
Поломка возможна при поломке всего api-proxy.

---

### zalogin
Авторизация пользователя.

#### Поля launch
```json
{
  "authorized": true,
  "id": "",
  "loyal": true,
  "phones": {},
  "uuid": "",
  "name": "",
  "phone": "",
  "token_valid": true,
  "yandex_staff": true
}
```
#### Запрос
`POST /v1/launch/auth`

[Существующая ручка](https://github.yandex-team.ru/taxi/uservices/blob/develop/services/zalogin/docs/yaml/api/launch.yaml)

#### Ответ
```json
{
  "authorized": true,
  "id": "",
  "loyal": true,
  "phones": {},
  "uuid": "",
  "name": "",
  "phone": "",
  "token_valid": true,
  "yandex_staff": true
}
```
#### Fallback policy
`PROPAGATE`

Авторизация критична для работы ручки

Конечный фолбэк обсудим по факту завершения

https://st.yandex-team.ru/TAXIDATA-1614


#### Retry policy
Ретраи на основе сервиса статистики

---

### User settings
Информация о пользовательских настройках

#### Поля launch
```json
{
  "user_settings_hash": ""
}
```

#### Запрос
```
GET /v1/settings

Headers:
- X-YaTaxi-PhoneId
```
#### Ответ
```json
{
  "user_settings_hash": ""
}
```
#### Fallback policy
Не добавлять поле в ответ

#### Retry policy
Обычные ретраи 3 раза

---

### Experiments
Старые и новые эксперименты вернет сервис экспериментов

#### Поля launch
```json
{
  "experiments": [],
  "typed_experiments": {}
}
```

#### Запрос
```
GET /v1/experiments

Headers:
- X-Yandex-UID
- X-YaTaxi-UserId
- X-Yandex-UUID
- X-YaTaxi-PhoneId
```
#### Ответ
```json
{
  "experiments": [],
  "typed_experiments": {}
}
```
#### Fallback policy
Подставить пустой ответ

```json
{
  "experiments": [],
  "typed_experiments": {}
}
```

#### Retry policy
Ретраи на основе сервиса статистики

---

### Antifraud
Информацию о пользовательских блокировках вернет сервис антифрода.

#### Поля launch
```json
{
  "blocked": {}
}
```

#### Запрос
```
GET /v1/block

Params:
- user_id
- user_phone_id
- device_id
```
#### Ответ
```json
{
  "blocked": {}
}
```

#### Fallback policy
Не добавлять поле в ответ

#### Retry policy
Ретраи на основе сервиса статистики

---

### Debts

#### Поля launch
```json
{
  "payment_statuses_filters": []
}
```

#### Запрос
```
GET /internal/launch/payment_filters

Params:
- phone_id
- brand
```
#### Ответ
```json
{
  "payment_filters": []
}
```
#### Fallback policy
Пустой список
```json
{
  "payment_filters": []
}
```

#### Retry policy
Ретраи на основе сервиса статистики

---

### Coupons
Информация о доступности реферальной программы

#### Поля launch
```json
{
  "can_generate_referrals": true
}
```

#### Запрос
```
GET /v1/referral

Headers:
- X-Yandex-UID
- X-YaTaxi-UserId
- X-YaTaxi-PhoneId
```

#### Ответ
```json
{
  "can_generate_referrals": false
}
```
#### Fallback policy
Не добавлять поле в ответ

#### Retry policy
Обычные ретраи 3 раза

---

### Support chat
Информация о коммуникации с поддержкой

#### Поля launch
```json
{
  "chat": {}
}
```

#### Запрос
```
GET /v1/support-chat

Headers:
- X-Yandex-UID
- X-YaTaxi-UserId
- X-YaTaxi-PhoneId
```
#### Ответ
```json
{
  "chat": {}
}
```
#### Fallback policy
Не добавлять поле в ответ

#### Retry policy
Обычные ретраи 3 раза

---

### Geofences

#### Поля launch
```json
{
  "geofences_tag": {}
}
```

#### Запрос
```
GET /v1/geofence-tag

Headers:
- X-YaTaxi-PhoneId
```
#### Ответ
```json
{
  "geofences_tag": {}
}
```
#### Fallback policy
Не добавлять поле в ответ

#### Retry policy
Обычные ретраи 3 раза

---

### Plus
Информация о пользовательских брендингах

#### Поля launch
```json
{
  "brandings": []
}
```

#### Запрос
```
GET /v1/brandings

Headers:
- X-Yandex-UID
- X-YaTaxi-UserId
- X-YaTaxi-Pass-Flags
```

#### Ответ
```json
{
  "brandings": []
}
```
#### Fallback policy
Пустой список
```json
{
  "brandings": []
}
```
#### Retry policy
Обычные ретраи 3 раза

---

### Eulas
Информация о пользовательских соглашениях

#### Поля launch
```json
{
  "need_acceptance": []
}
```

#### Запрос
```
GET /v1/launch/list

Headers:
- X-Yandex-UID
- X-YaTaxi-UserId
- X-YaTaxi-Pass-Flags
- X-Real-Ip
```

#### Ответ
```json
{
 "need_acceptance": []
}
```
#### Fallback policy
Пустой список
```json
{
  "need_acceptance": []
}
```

#### Retry policy
Обычные ретраи 3 раза

---

### Regional policy
Информация о региональных параметрах

#### Поля launch
```json
{
  "parameters": {}
}
```

#### Запрос
```
GET /v1/regional_policy

Params:
- country_code

Headers:
- X-Real-IP
```
#### Ответ
```json
{
  "parameters": {}
}
```
#### Fallback policy
Пустой объект
```json
{
  "parameters": {}
}
```
#### Retry policy
Обычные ретраи 3 раза

---

### Order-core
Информация о текущих заказах.

#### Поля launch
```json
{
  "orders_state": {
    "orders": []
  },
  "orders": []
}
```

#### Запрос
```
GET /v1/tc/active-orders
Params:
- userid
Headers:
- X-Yandex-UID
```
#### Ответ
```json
{
  "orders_state": {
    "orders": []
  },
  "orders": []
}
```
#### Fallback policy
`PROPAGATE`

Интерфейс не должен флапать. 
Если заказ активен -- нужно показывать карточку заказа.

#### Retry policy
Ретраи на основе сервиса статистики

---

### Multiorder
Информация о доступности мультизаказа

#### Поля launch
```json
{
  "orders_state": {
    "can_make_more_orders": true,
    "no_more_orders_reason": ""
  }
}
```

#### Запрос
```
GET /v1/multiorder/state
Headers:
- X-Yandex-UID
- X-YaTaxi-PhoneId
- X-YaTaxi-UserId
- X-Real-Ip
```
#### Ответ
```json
{
  "can_make_more_orders": "allowed",
  "no_more_orders_reason": ""
}
```
#### Fallback policy
Возможность мультизаказа
```json
{
  "can_make_more_orders": "allowed"
}
```

В случае, если supported_features не содержит multiorder
необходимо запретить мультизаказ
```json
{
  "can_make_more_orders": "disallowed"
}
```


#### Retry policy
Обычные ретраи 3 раза

---

### Feedback
Информация о необходимости запросить фидбек

#### Поля launch
```json
{
  "ask_feedback": {}
}
```

#### Запрос
```
GET /v1/ask_feedback

Headers:
- X-Yandex-UID
- X-YaTaxi-PhoneId
- X-YaTaxi-UserId
```
#### Ответ
```json
{
  "ask_feedback": {}
}
```
#### Fallback policy
Не добавлять поле в ответ

#### Retry policy
Обычные ретраи 3 раза

---

### Passenger-profile
Профиль пользователя

#### Поля launch
```json
{
  "passenger_profile": {}
}
```

#### Запрос
`GET /passenger-profile/v1/profile`
#### Ответ
```json
{
 "passenger_profile": {}
}
```
#### Fallback policy
Не добавлять поле в ответ

#### Retry policy
Обычные ретраи 3 раза

---

## Запись в launch

### Eulas
Необходимо запоминать принятые соглашения.
Запись нужно делать асинхронно, поэтому ручка должна поставить stq таск
и быстро ответить.

#### Запрос
```
GET /v1/launch/accept

Headers:
- X-YaTaxi-UserId
- X-YaTaxi-PhoneId
```

#### Ответ
200 Ok

#### Fallback policy
`PROPAGATE`

Необходимо зарегистрировать принятие соглашения пользователем.
Вероятность отказа крайне невысока.

#### Retry policy
Обычные ретраи 3 раза

---

## zalogin
https://st.yandex-team.ru/TAXIDATA-1614

В сервис залогин переезжает

- Создание пользователя
- Сложная логика обновления пользователя
- phone confirmations
- Миграция geo коллекций (UserEmailBindYandexUid, UserPhoneBindYandexUid)

---


## Полный перечень необходимых микросервисов
+ api-proxy
+ zalogin
+ User settings
+ Experiments
+ Antifraud
+ Debts
+ Coupons
+ Support chat
+ Geofences
+ Plus
+ Eulas
+ Regional policy
+ Order-core
+ Multiorder
+ Feedback
+ Passenger-profile

## Тайминги
####Сейчас:

На основе кластера taxi_api.
Большинство из данных тяжелых операций выполняются последовательно.
api-proxy, распараллелив запросы, должно уменить тайминги. 
```
launch_timings timings in ms (on 1905 entries):
                                                   p99

build_can_make_more_orders_time                  0.000
fetch_unfinished_orders_time                     0.000
record_launch_time                               0.007
parse_request_time                               0.065
launch_get_passenger_profile_time                0.128
migrate_geo_collections_time                    45.661
fetch_portal_account_confirmations_tim          21.629
load_chat_messages_time                         19.092
ensure_phones_docs_existance_time               47.724
get_phones_docs_time                            35.010
auth_phonish_user_time                          42.382
update_phones_confirmations_time                12.125
launch_build_experiments3_result_time            8.952
ensure_phone_ids_existance_time                 86.955
auth_get_uid_info_time                          12.009
build_response_time                             26.618
get_feedback_time                               31.222
parallel_getting_ya_plus_time                   26.487
load_geofences_tag_time                         11.072
fetch_portal_confirms_time                     264.856
auth_portal_user_time                          265.175
auth_mongo_queries_time                        417.701
auth_time                                      455.072
get_launch_orders_time                         193.629
orders_mongo_queries_time                      570.956 
other_data_time                                570.974 

total_time                                    1151.823
```

####Тайминги типовых сервисов 

Было проведено исследование типовых высоконагруженных сервисов c++ и py3. 
```
p99 debts (uservices) - 50ms
p99 zalogin (uservices) - 400ms
p99 coupons (uservices) - 300ms

p99 tariffs (backend-py3) - 15ms
p99 personal-goals (backend-py3) - 60ms
p99 billing-accounts (backend-py3) - 212ms
p99 order-performer (backend-py3) - 100ms
```
Таким образом, необходимости в отказе от python3 нет.

####Планируемые ограничения:
```
Максимальный суммарный таймаут - 800ms
```

## Мониторинг
Мониторинг зависимостей launch будет в графане.
На дашборде будут отображены все зависимости лонч с OK rps, BAD rps, Timings.
В api-proxy подобный дашборд умеет генерироваться, пример:

https://grafana.yandex-team.ru/d/gM9vgN4Wz/taxi_conductor_taxi_api_proxy

## Алертинг

api-proxy отсылает метрики в сервис статистики.
Сервис статистики автоматически генерирует juggler-конфиги и инициирует проверки monrun для каждого сервиса.
Это позволяет подписаться на фолбэки нужные полей в лонче

Более подробно тут:
 
https://wiki.yandex-team.ru/taxi/backend/architecture/statistics/how-to/#monitoringi
