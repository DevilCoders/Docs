# API административного интерфейса


### Контроль заказа

```
GET {{host_admin}}/api/admin/request/list?employer=<employer_code>
```

Возвращает список активных заказов. Возможна фильтрация по `employer_code`. Получить список известных партнеров-заказчиков можно через [employers](employers.md)

Пример ответа
```
"has_more": false,
"history": [
    {
                "history_action": "add",
                "employer_code": "default",
                "request_code": "177eabb5-fea3-4c26-85b4-42e89b67fa59",
                "decision_deadline": "1600688160",
                "request_id": "f4531c89-fc8f-45cd-b846-40f0f6b47694",
                "history_timestamp": 1600687821,
                "revision": "4710",
                "history_user_id": "segments_journal"
    },
]
```

Зная идентификатор заказа можно получить полную детализация по активному заказу (как только обработка заказа завершается, ручка отдаст 404, за подробными данными по выполненным заказам смотреть в ручке `history`)
Поддерживается постраничная отдача данных через параметры `offset` и `limit`.

```
GET {{host_admin}}/api/admin/request/get?request_id=<request_id>
```

Пример ответа (**стандартный полный репорт заказа**)

- employer - партнер-заказчик, в рамках флоу котрого осуществляется доставка.
- canceled - сстояние отмененной заявки.
- resources_info - секция товаров к доставке.
    - resources_info.events_chain - цепочка выполнения заказа. Последовательность узлов (типы узла определяются признаком `TYPE`). В зависимости от типа у узла может быть разный набор полей.
    - resources_info.resource - текущее состояние ресурса.
        - resources_info.resource.node_id - в кaком узле он сейчас находится (между узлами там будет пусто)
        - resources_info.resource.performer_id - идентификатор курьера, если какой-то курьер забрал ресурс
        - resources_info.resource.features - свойства ресурса, используемые при назначении.


Возможны три типа узлов
- NODE - точка размещения ресурса. Это склад, конечный пользователь-получатель, склад промежуточного хранения, точка передачи между курьерами.
- ACTION - действи с ресурсом (забрать или положить в точку размещения)
- TRANSFER - переходное между двумя action  действие ("курьер везет")

```
 {
    "employer": "eats",
    "canceled": false,
    "request_id": "56f23c8c-748c-4ad1-bff2-6d6b81162c58",
    "resources_info": [
        {
            "events_chain": [
                {
                    "node_id": "3f44b302-25c4-4ba1-a81a-448b97e6f166",
                    "implementation": {
                        "class_name": "tmp",
                        "coord": {
                            "lat": 55.73552,
                            "lon": 37.642474
                        },
                        "details": {}
                    },
                    "type": "NODE",
                    "snapshot_revision": 29572,
                    "code": "a9527173a0e947b2b221231b2c3b925a"
                },
                {
                    "contractor_id": "",
                    "status": "waiting",
                    "action_id": 9765,
                    "type": "ACTION"
                },
                {
                    "transfer_id": "445a2f56-6189-411a-869f-b238afd10871",
                    "status": "waiting",
                    "enabled": true,
                    "type": "TRANSFER"
                },
                {
                    "requested_action_type": "put_resource",
                    "resource_id": "6302e25d-93e2-45fb-94fc-4fa47417be7b",
                    "contractor_id": "",
                    "status": "waiting",
                    "action_id": 9764,
                    "type": "ACTION",
                    "contractor_session_id": ""
                },
                {
                    "node_id": "ffb9cd15-5b32-46a0-a3a2-769bbf384c10",
                    "implementation": {
                        "class_name": "tmp",
                        "coord": {
                            "lat": 55.737542,
                            "lon": 37.641135
                        },
                        "details": {}
                    },
                    "type": "NODE",
                    "snapshot_revision": 29572,
                    "code": "19259f34af3845e3b9fc0702172dfb69"
                }
            ],
            "resource": {
                "node_id": "3f44b302-25c4-4ba1-a81a-448b97e6f166",
                "resource_id": "6302e25d-93e2-45fb-94fc-4fa47417be7b",
                "resource_code": "0c9dbfa09090483eb028831082b0b8f0",
                "perform_instant": 1598511865,
                "performer_id": "",
                "features": [
                    {
                        "resource_classes_feature": {
                            "classes": [
                                "courier",
                                "eda",
                                "lavka"
                            ]
                        },
                        "class_name": "classes"
                    },
                    {
                        "taxi_requirements": {
                            "true_req": [
                                "door_to_door"
                            ]
                        },
                        "class_name": "taxi_requirements"
                    }
                ]
            }
        }
    ],
    "revision": 29572,
    "request_code": "e39d6190-6d48-4e4e-afe7-efa18fb2b879"
}
```

```
POST {{host_admin}}api/admin/request/cancel?request_id=<request_id>
```

Используется для ручной отмены заказа оператором.


### Курьерские сессии

Получение текущей сессии исполнителя. Это текущая точка исполнителя + набор действие, которые ему еще предстоит сделать;

```
GET {{host_admin}}/api/admin/contractor/session?contractor_id=<c_id>
```

Получени истории по сессии - это набор действий в сессии, который уже был пройден исполнителем

```
GET {{host_admin}}/api/admin/contractor/session/history?contractor_id=<c_id>&session_id=<session_id>&sice=<timestamp>
```
- session_id - показывает выполненные действия в заданной сессии (по сути - маршрутном листе)
- c_id - показывает выполненные действия исполнителя (несколько предыдущих сессий)
- since - время в секунда для отсечки снизу (по-молчанию - 3 дня)

Чтобы посомотреть историю действий исполнителя, нужно взять его текщую сессия + история по session_id


### Станции

Поулчение списка зарегистрированных станций.


```
GET {{host_admin}}/api/admin/station/list
```

Пример ответа:

```
{
    "stations": [
        {
            "operator_station_id": "svyaznoy-1",
            "location": [
                37.621806,
                55.755569
            ],
            "deprecated": false,
            "enabled": true,
            "location_details": {
                "street": "Ветошный пер.",
                "floor": "",
                "sub_region": "",
                "locality": "",
                "country": "Россия",
                "porch": "",
                "housing": "",
                "building": "",
                "house": "9",
                "metro": "Театральная",
                "settlement": "",
                "room": "",
                "region": "Москва",
                "intercom": "",
                "district": "Центр"
            },
            "station_id": "4075a917-3935-486c-9334-e9dfa0b14919",
            "operator_id": "svyaznoy",
            "station_name": "Связной",
            "station_full_name": "Тестовый магазин Связной",
            "description": "Тестовый магазин Связной"
        },
}
```

Регистрация новой станции или обновление данных существующей

```
POST {{host_admin}}/api/admin/station/upsert
{
    "class_name": "warehouse",
    "warehouse": {
        "volume_by_week": [
            40,
            40,
            40,
            10,
            20,
            30,
            40
        ]
    },
    "operator_station_id": "svyaznoy-1",
    "station_name": "Связной",
    "station_full_name": "Тестовый магазин Связной",
    "enabled": true,
    "description": "Тестовый магазин Связной",
    "location": [
        37.621806,
        55.755569
    ],
    "location_details": {
        "street": "Ветошный пер.",
        "floor": "",
        "sub_region": "",
        "locality": "",
        "country": "Россия",
        "porch": "",
        "housing": "",
        "building": "",
        "house": "9",
        "metro": "Театральная",
        "settlement": "",
        "room": "",
        "region": "Москва",
        "intercom": "",
        "district": "Центр"
    }
}
```


### Управление сервисом


#### Схемы
```
GET {{host_admin}}/api/admin/constant
```

Список основных констант для выполнения подстановок в админке. В сновном это [схемы](scheme.md), для основных объектов.
- iface_notifiers
- iface_rt_background_state
- iface_rt_background_state


#### Settings

Используются для установки реалтайм-параметров некоторых процессов. А также для конфигурации хендлеров.

Получение списка настроек

```
GET {{host_admin}}/api/settings/info
```

Пример ответа

```
{
    "settings": [
        {
            "setting_key": "candidates.max_distance",
            "setting_value": "10000"
        },
        {
            "setting_key": "graph_api.straight_distances.enabled",
            "setting_value": "false"
        }
    ]
}
```

Обновление или заведение новой настройки.

В данном примере заводится новая ручка API.

```
POST {{host_admin}}/api/settings/upsert
{
	"settings":[
        {
            "setting_key": "handlers.api/admin/constant",
            "setting_value": "ProcessorType: service-constant \n AuthModuleName: fake"
        }
    ]
}
```
