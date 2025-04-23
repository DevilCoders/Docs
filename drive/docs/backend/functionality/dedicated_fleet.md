# Заявка на выделенный парк

Заявка на выделенный парк содержит информацию о выд. парке организации

## Офферы

### Оффер `dedicated_fleet_offer`

Содержит общие условия владения парком, а так же массив `dedicated_fleet_unit_offer`

### Оффер `dedicated_fleet_unit_offer`

Описывает индивидуальные условия и опции по конкретной машине в парке.

## Билдеры

### Билдер `dedicated_fleet_offer_builder`

Билдер для построения оффера для выд. парка. В админке задаётся как `Action` с типом
`dedicated_fleet_offer_builder`.

Конфигурация билдера:

* `offer_holder_tag` &mdash; название тега, который будет навешен на организацию при букинге с данными по заявке (обязательное поле).

* `unit_offer_builder` &mdash; название билдера, который будет использоваться для построения заявки на машину в выделенном парке (обязательное поле).

### Билдер `dedicated_fleet_unit_offer_builder`

Билдер для построения оффера для единицы(машины) выд. парка. В админке задаётся как `Action` с типом
`unit_offer_builder`.

Конфигурация билдера:

* `delta_cost` &mdash; цена владения (копейки) (обязательное поле).

* `???` &mdash; на данный момент билдер поддерживает только стоимость владения.

## Теги

### Тег заявки `dedicated_fleet_offer_holder_tag`

Тег навешивается на организацию при подтверждении заявки(букинге), в нем хранится оффер, в теге реализованна логика поведения на событие обновления,
это позволяет менять параметры оффера (добавлять/удалять/изменять машины и их свойства).

Поля тега:

* `communication_tag` &mdash; название тега, который будет навешен на пользователя оформившего заявку выд. парка (обязательное поле).
* `fleet_tag` &mdash; название тега, который будет навешен на автомобили выд. парка (обязательное поле).
* `evolve_target_suffix` &mdash; суффикс с которым будут эволюционированные теги указанные в `tags_to_evolve_with_suffix` (default `_dedicated_fleet`).
* `tags_to_evolve_with_suffix` &mdash; теги, которые нужно эволюционировать с суффиксом `evolve_target_suffix`.
* `car_tags` &mdash; дополнительные теги, которые навесятся на машину при добавлении к выд.парку.

* `construct_offer` &mdash; флаг для создания оффера, полезно при навешивании тега заявки через админку.
* `fleet_size` &mdash; задает размер выд.парка, если 'construct_offer' выставлен в true.
* `builder` &mdash; тип оффер билдера, если 'construct_offer' выставлен в true.

Примечание для `evolve_target_suffix` и `tags_to_evolve_with_suffix` типы тегов в которые необходимо эволюционировать не создаются, перед назначением суффикса и задания списка тегов для эволюции,
необходимо убедиться что такие типы уже зарегистрированы, в противном случае результатом станет ошибка.

### Тег коммуникации `dedicated_fleet_support_tag`

Тег навешивается на пользователя драйва, который оформил выд. парк для организации, по этому тегу создается чат саппорта по аналогии с долгосроком, где будет возможность управлять парком.

Поля тега:

* `linked_tag_id` &mdash; id тега заявки на выд. парк на организации.


### Тег машины выд. парка `special_fleet_tag`

Тег навешиваемый на машину добавленную к выделенному парку

## Ручки

### Ручка `/api/yandex/offers/create`

Отвечает за построение оффера выд. парка.

#### Get параметры

* `offer_name` &mdash; id доступного для построения оффера выд. парка. Обязательное поле.

#### JSON BODY

```
{
    "variables": {
        "count": 10,
        "since": 1646321543,
        "until": 1648989135,
        "account_id": 1,
        "tariff_plan": "plan_id",
        "options":{
            "remove_wrap": true,
            "fueling": true
        }
    }
}
```

* `fleet_unit_parameters` &mdash; массив конфигураций по каждой машине выд. парка, на данный момент схемы для этого элемента нет, используется только для указания количества машин. Обязательное поле.
* `since` &mdash; дата ввода выд. парка в эксплуатацию(нужно для расчета предварительной стоимости). Обязательное поле.
* `until` &mdash; дата вывода выд. парка из эксплуатации(нужно для расчета предварительной стоимости). Обязательное поле.
* `account_id` &mdash; id организации для которой формируется заявка. Обязательное поле.

#### Ответ ручки

В ответе возвращается поля похожие на поля стандартного оффера дополненные массивом офферов для каждой единицы выд. парка:
* `total_cost` &mdash; суммарная стоимость владения парком.
* `units_offers/holding_cost` &mdash; стоимость владения единицей парка.
* `units_offers/total_cost` &mdash; полная стоимость владения единицей парка со всеми опциями.
* `units_offers/offer_id` &mdash; id юнит оффера(валиден только относительно родительского оффера).
* `car_id` &mdash; id машины выд. парка, привязанной к юнит офферу(в начале это поле пустое, значение можно задать через тег коммуникации).

##### Примеры запросов

Запрос:

```(bash)
curl 'https://testing.carsharing.yandex.net/api/yandex/offers/create?offer_name=simple_dedicated_fleet_offer_name' -X GET -H 'Authorization: OAuth XXX'
    -d '{"variables": {"fleet_unit_parameters": [{},{},{},{}],"since": 1646321543, "until": 1648989135, "account_id": 1}}'
```

Ответ:

```
"offers": [
    {
        "name": "simple_dedicated_fleet_offer",
        "price_constructor_id": "simple_dedicated_fleet_offer",
        "device_id": "",
        "group_name": "",
        "account_id": 1,
        "units_offers": [
            {
                "constructor_id": "simple_dedicated_fleet_unit_offer",
                "is_corp_session": false,
                "type": "dedicated_fleet_unit_offer",
                "car_id": "",
                "total_cost": 444598667,
                "device_id": "",
                "holding_cost": 444598667,
                "behaviour_constructor_id": "simple_dedicated_fleet_unit_offer",
                "deadline": 1651358133,
                "name": "simple_dedicated_fleet_unit_offer",
                "group_name": "",
                "price_constructor_id": "simple_dedicated_fleet_unit_offer",
                "offer_id": "077c729e-023f-f3c3-eb3e-ae4e26f36e55",
                "localizations": {},
                "duration": 2667592000000,
                "is_plus_user": false,
                "wallets": []
            },
            {
                "constructor_id": "simple_dedicated_fleet_unit_offer",
                "is_corp_session": false,
                "type": "dedicated_fleet_unit_offer",
                "car_id": "",
                "total_cost": 444598667,
                "device_id": "",
                "holding_cost": 444598667,
                "behaviour_constructor_id": "simple_dedicated_fleet_unit_offer",
                "deadline": 1651358133,
                "name": "simple_dedicated_fleet_unit_offer",
                "group_name": "",
                "price_constructor_id": "simple_dedicated_fleet_unit_offer",
                "offer_id": "0ea8a360-96ad-6a8f-138a-ecb18ff891a1",
                "localizations": {},
                "duration": 2667592000000,
                "is_plus_user": false,
                "wallets": []
            },
            {
                "constructor_id": "simple_dedicated_fleet_unit_offer",
                "is_corp_session": false,
                "type": "dedicated_fleet_unit_offer",
                "car_id": "",
                "total_cost": 444598667,
                "device_id": "",
                "holding_cost": 444598667,
                "behaviour_constructor_id": "simple_dedicated_fleet_unit_offer",
                "deadline": 1651358133,
                "name": "simple_dedicated_fleet_unit_offer",
                "group_name": "",
                "price_constructor_id": "simple_dedicated_fleet_unit_offer",
                "offer_id": "8f3c618b-30ab-ca0b-931a-92fecc0cc1ad",
                "localizations": {},
                "duration": 2667592000000,
                "is_plus_user": false,
                "wallets": []
            },
            {
                "constructor_id": "simple_dedicated_fleet_unit_offer",
                "is_corp_session": false,
                "type": "dedicated_fleet_unit_offer",
                "car_id": "",
                "total_cost": 444598667,
                "device_id": "",
                "holding_cost": 444598667,
                "behaviour_constructor_id": "simple_dedicated_fleet_unit_offer",
                "deadline": 1651358133,
                "name": "simple_dedicated_fleet_unit_offer",
                "group_name": "",
                "price_constructor_id": "simple_dedicated_fleet_unit_offer",
                "offer_id": "ee047e58-6057-56ba-c508-8cc62b8fede0",
                "localizations": {},
                "duration": 2667592000000,
                "is_plus_user": false,
                "wallets": []
            }
        ],
        "is_plus_user": false,
        "total_cost": 1778394668,
        "localizations": {},
        "constructor_id": "simple_dedicated_fleet_offer",
        "offer_id": "24ccacec-50de-80bd-be0e-9dc9f8099eff",
        "wallets": [],
        "type": "dedicated_fleet_offer",
        "list_priority": 0,
        "behaviour_constructor_id": "simple_dedicated_fleet_offer",
        "prices": null,
        "is_corp_session": false,
        "payment_methods": [],
        "deadline": 1651358133
    }
]
```

### Ручка `/b2b/sessions/dedicated_fleet`

Ручка получения информации о сессиях владения выд. парка.

#### Параметры

* `account_id` &mdash; id аккаунта. Обязательное поле.
* `session_id` &mdash; id сессии. Обязательное поле.

#### JSON BODY

Отсутствует.

#### Ответ ручки

В ответе возвращается стандартное описание сессий, добавлен массив сессий владения по `special_fleet_tag`:
* `sessions/compilation/session/specials/units` &mdash; маcсив сессий владения по всем машинам, которые когда либо были в выд. парке.
* `.../units/.../actual` &mdash; указывает на то: находиться ли машина сейчас в выд. парке или нет.
* `.../units/.../add_ts` &mdash; дата добавления машины в парк.
* `.../units/.../remove_ts` &mdash; дата вывода машины из парке.

##### Примеры запросов

Запрос:

```(bash)
curl 'https://testing.carsharing.yandex.net/b2b/sessions/dedicated_fleet?session_id=62283f2e-c81d-2d9e-a120-4320cca4771d' -X GET -H 'Authorization: OAuth XXX'
```

Ответ:
```
{
    "sessions": [
        {
            // актуальный оффер 
            "offer":{
            },
            "events": {
                "timeline": [
                    {
                        "timestamp": 1651074292,
                        "action": "add",
                        "event_id": 1,
                        "user_id": "97b933ed-4145-400c-98cc-f0c755a12590"
                    },
                    {
                        "timestamp": 1651074306,
                        "action": "update_data",
                        "event_id": 2,
                        "user_id": "8b33b36b-ca2a-4f16-9af4-dc1598f02ec4"
                    },
                    {
                        "timestamp": 1651074313,
                        "action": "update_data",
                        "event_id": 3,
                        "user_id": "8b33b36b-ca2a-4f16-9af4-dc1598f02ec4"
                    }
                ],
                "meta": {
                    "start": 1651074292,
                    "last_event_id": 3,
                    "current": 1651074317,
                    "instance_id": "f7676935-04fe-27ae-e16c-69fcf1c28245",
                    "corrupted": false,
                    "session_id": "62283f2e-c81d-2d9e-a120-4320cca4771d",
                    "user_id": "97b933ed-4145-400c-98cc-f0c755a12590",
                    "object_id": "13548812",
                    "finished": false
                }
            },
            "compilation": {
                "session": {
                    "specials": {
                        "units": [
                            {
                                "events": [
                                    {
                                        "tag_id": "2c8894a8-8a5a-5302-49cc-e700f13c7ea4",
                                        "tag_details": {
                                            "offer_id": "62283f2e-c81d-2d9e-a120-4320cca4771d",
                                            "on_assign_evolved_tags": [],
                                            "tag": "special_fleet_tag",
                                            "priority": 0,
                                            "parent_id": 13548812,
                                            "unit_offer_id": "5e22058e-1470-1d8d-c5ea-d381e882db90",
                                            "on_assign_added_tags": [
                                                "02130831-c2d3-8db2-4005-a9b33282cafd"
                                            ]
                                        },
                                        "action": "add",
                                        "user_id": "8b33b36b-ca2a-4f16-9af4-dc1598f02ec4",
                                        "event_id": 4824911,
                                        "object_id": "4128e3f6-1bb0-8010-c919-641187d7b3a7",
                                        "timestamp": 1651074306,
                                        "tag_name": "special_fleet_tag"
                                    },
                                    {
                                        "tag_id": "2c8894a8-8a5a-5302-49cc-e700f13c7ea4",
                                        "tag_details": {
                                            "offer_id": "62283f2e-c81d-2d9e-a120-4320cca4771d",
                                            "on_assign_evolved_tags": [],
                                            "tag": "special_fleet_tag",
                                            "priority": 0,
                                            "parent_id": 13548812,
                                            "unit_offer_id": "5e22058e-1470-1d8d-c5ea-d381e882db90",
                                            "on_assign_added_tags": [
                                                "02130831-c2d3-8db2-4005-a9b33282cafd"
                                            ]
                                        },
                                        "action": "remove",
                                        "user_id": "8b33b36b-ca2a-4f16-9af4-dc1598f02ec4",
                                        "event_id": 4824915,
                                        "object_id": "4128e3f6-1bb0-8010-c919-641187d7b3a7",
                                        "timestamp": 1651074313,
                                        "tag_name": "special_fleet_tag"
                                    }
                                ],
                                "compilation": {
                                    "session": {
                                        "specials": {
                                            "remove_ts": 1651074313000,
                                            "car_id": "4128e3f6-1bb0-8010-c919-641187d7b3a7",
                                            "unit_offer_id": "5e22058e-1470-1d8d-c5ea-d381e882db90",
                                            "add_ts": 1651074306000,
                                            "actual": "0"
                                        }
                                    }
                                }
                            },
                            {
                                "events": [
                                    {
                                        "tag_id": "778c8fbb-077b-e508-3ef2-ab37acfbcbfc",
                                        "tag_details": {
                                            "offer_id": "62283f2e-c81d-2d9e-a120-4320cca4771d",
                                            "on_assign_evolved_tags": [],
                                            "tag": "special_fleet_tag",
                                            "priority": 0,
                                            "parent_id": 13548812,
                                            "unit_offer_id": "72eb1f7e-53c4-38ce-6cf4-f8137341d08c",
                                            "on_assign_added_tags": [
                                                "1704f74c-29fc-e16a-a396-2974f92913bb"
                                            ]
                                        },
                                        "action": "add",
                                        "user_id": "8b33b36b-ca2a-4f16-9af4-dc1598f02ec4",
                                        "event_id": 4824913,
                                        "object_id": "921c0948-1524-a7ff-73bc-0f3ce5206b03",
                                        "timestamp": 1651074306,
                                        "tag_name": "special_fleet_tag"
                                    }
                                ],
                                "compilation": {
                                    "session": {
                                        "specials": {
                                            "remove_ts": 18446744073709551,
                                            "car_id": "921c0948-1524-a7ff-73bc-0f3ce5206b03",
                                            "unit_offer_id": "72eb1f7e-53c4-38ce-6cf4-f8137341d08c",
                                            "add_ts": 1651074306000,
                                            "actual": "1"
                                        }
                                    }
                                }
                            }
                        ],
                        "actual_car_ids": [
                            "921c0948-1524-a7ff-73bc-0f3ce5206b03"
                        ],
                        "session_tag_id": "f7676935-04fe-27ae-e16c-69fcf1c28245",
                        "session_id": "62283f2e-c81d-2d9e-a120-4320cca4771d",
                        "account_id": "13548812"
                    }
                }
            }
        }
    ]
}
```

### Ручка `/b2b/dedicated_fleet/session/drop`

Ручка отмены заявки. Для отмены все машины будут автоматически выведены из выделенного парка, теги, которые эволюционировались с суффиксом и приезжали, с тегом выделенного парка, будут возвращены в исходное состояние.

#### Параметры

* `session_id` &mdash; id сессии. Обязательное поле.

#### JSON BODY

Отсутствует.

##### Примеры запросов

Запрос:

```(bash)
curl 'https://testing.carsharing.yandex.net/b2b/dedicated_fleet/session/drop?session_id=62283f2e-c81d-2d9e-a120-4320cca4771d' -X GET -H 'Authorization: OAuth XXX'
```

Ответ:

Отсутствует.

## Назначение машин

Назначение машин происходит через эволюционирование тега коммуникации `dedicated_fleet_support_tag`, что приведет к обновлению тега `dedicated_fleet_offer_holder_tag` и офферу, который в нем хранится.
При эволюции (`/api/yandex/tag/evolve?tag_id=<tag id>`) нужно задать необходимую нагрузку. Ключ элемента это id юнит оффера, который можно вытащить из репорта оффера выд. парка `offers/units_offers/[offer_id]`, таким
образом каждый car_id уникально привязан к id юнит оффера.

```
{
    "ee047e58-6057-56ba-c508-8cc62b8fede0": {   //unit offer id
        "car_id": "xxx-xxx-xxx"     //привязать машину к юнит офферу
    },
    "8f3c618b-30ab-ca0b-931a-92fecc0cc1ad": {   //unit offer id
        "car_id": "yyy-yyy-yyy"     //привязать машину к юнит офферу
    },
    "077c729e-023f-f3c3-eb3e-ae4e26f36e55": {   //unit offer id
        "car_id": "",               //удалить связь машины и юнит оффера
        "force_update": "true"      //при ошибке проверки тегов позволяет пропустить внутренние проверки и убрать машину из выд. парка
    }
}
```

В теге коммуникации есть `linked_tag_id` id тега заявки на выд. парк, по этому id можно получить актуальную информацию о состоянии парка.

### Примеры запросов

Запрос:

```(bash)
curl 'https://testing.carsharing.yandex.net/api/yandex/tag/evolve?tag_id=<tag_id>' -X GET -H 'Authorization: OAuth XXX'
    -d '{"ee047e58-6057-56ba-c508-8cc62b8fede0": {"car_id": "xxx-xxx-xxx"},"8f3c618b-30ab-ca0b-931a-92fecc0cc1ad": {"car_id": "yyy-yyy-yyy"},"077c729e-023f-f3c3-eb3e-ae4e26f36e55": {"car_id": ""}}'
```

Ответ:

Отсутствует.


## Front API

Расширенная выдача оффера с описанием полей для построения интерфейса на фронте traits=ReportOfferDetails

```
{
    "data": {
        "payment_methods": [
            {
                "name": "0257",
                "group_type": "radio",
                "icon": "",
                "type": "credit_card",
                "request_parameters": {
                    "card": "card-x12345",
                    "account_id": "card"
                },
                "selected": true
            }
        ],
        "sf": [],
        "poi": [],
        "accounts": [
            {
                "name": "За свои",
                "icon": "",
                "balance": 0,
                "id": "card"
            }
        ],
        "clusters": [],
        "offers": [
            {
                "prebill": [ // предварительный чек аренды, формат такой же, как и у чека в конце поездки
                    {
                        "duration": 2678400,
                        "details": "3 месяца и 2 дня",
                        "type": "unit_builder",
                        "title": "Тариф Ларгусы»",
                        "cost": 100031
                    },
                    {
                        "details": "Аренда 10 Ларгусов",
                        "type": "count",
                        "title": "dedicated_fleet_offer.count.title",
                        "count": 10,
                        "cost": 99999999
                    },
                    {
                        "details": "Дополнительные опции",
                        "type": "options_total",
                        "title": "dedicated_fleet_offer.options_total.title",
                        "cost": 99999999
                    },
                    {
                        "type": "total",
                        "title": "Итого",
                        "cost": 9999999999
                    }
                ],
                "name": "simple_dedicated_fleet_offer",
                "price_constructor_id": "simple_dedicated_fleet_offer",
                "device_id": "",
                "group_name": "",
                "model_title": "dedicated_fleet_offer.model_title",
                "model_subtitle": "dedicated_fleet_offer.model_subtitle", // не null для пакетов
                "primary": [
                    {
                        "value": 2, // текущее количество машин
                        "subtitle": "В наличии 10 машин", // available count loc
                        "default_value": "10",
                        "unit": "",
                        "title": "dedicated_fleet_offer.count.title",
                        "minimal_value": 1,
                        "cost": null, 
                        "type": "integer", // тип – целочисленная переменная
                        "predicted_cost": null,
                        "id": "count",
                        "maximal_value": 10 // считаем количество доступных машин через тег фильтр по модельному тегу, но не более максимального значения из билдера
                    },
                    {
                        "value": null,
                        "subtitle": "dedicated_fleet_offer.start_ts.subtitle",
                        "default_value": 1652812416,
                        "unit": "",
                        "title": "dedicated_fleet_offer.start_ts.title",
                        "minimal_value": 1652812416,
                        "cost": null,
                        "type": "integer",
                        "predicted_cost": null,
                        "id": "start_ts",
                        "maximal_value": 1652812416
                    },
                    {
                        "value": null,
                        "subtitle": "dedicated_fleet_offer.end_ts.subtitle",
                        "default_value": 1752812416,
                        "unit": "",
                        "title": "dedicated_fleet_offer.end_ts.title",
                        "minimal_value": 1752812416,
                        "cost": null,
                        "type": "integer",
                        "predicted_cost": null,
                        "id": "end_ts",
                        "maximal_value": 1752812416
                    },
                    {
                        "value": null,
                        "subtitle": "dedicated_fleet_offer.duration.subtitle", // локализация срока аренды <3 месяца и 2 дня>
                        "default_value": 5000400,
                        "unit": "",
                        "title": "dedicated_fleet_offer.duration.title", // Срок аренды
                        "minimal_value": 5000400,
                        "cost": null,
                        "type": "integer",
                        "predicted_cost": null,
                        "id": "duration",
                        "maximal_value": 9999999999
                    }
                ],
                // базовый конструктор офферов по машинам, тут описаны условия и опции общие для всех моделей указанных в предложении\тарифе\пакете 
                // позволяет упростить оформление заявки если пользователь не хочет конфигурировать машины отдельно
                // в текущем варианте в массиве будет один элемент так как дизайн не поддерживает настройку машин или пакетов
                "unit_builder": {
                    "constructor_id": "simple_dedicated_fleet_unit_offer",
                    "type": "dedicated_fleet_unit_offer",
                    "total_cost": 440000,
                    "device_id": "",
                    "holding_cost": 440000, // стоимость владения единицей парка (копейки)
                    "behaviour_constructor_id": "simple_dedicated_fleet_unit_offer",
                    "deadline": 1646409312,
                    "name": "simple_dedicated_fleet_unit_offer",
                    "group_name": "",
                    "price_constructor_id": "simple_dedicated_fleet_unit_offer",
                    "offer_id": "5f4ad46a-2854-8099-317e-591641e02034",
                    "localizations": {},
                    "duration": 2667592000,
                    // набор дополнительных опций
                    // в интерфейсе отображаются после указания срока аренды
                    // опции применяются ко всем машинам которые будут в парке
                    // указаны только те опции, которые можно применить ко всем машинам, настраиваются через массив в админке
                    // структура элемента аналогична структуре элементов блоков primary и secondary в долгосроке
                    // от механизма расчета опции будет зависть отображаемая стоимость и включение её в предварительный и итоговый счет
                    "secondary": [
                        // опция содрать оклейку имеет только стоимость включения, эта опция разовая, её стоимость будет включена в итоговый чек
                        {
                            "value": null, // текущее значение в оффере
                            "subtitle": "dedicated_fleet_offer.remove_wrap.subtitle", // текст серым
                            "default_value": false, // значение по умолчанию - использовать, если value == null
                            "unit": "руб", // единица измерения переменной
                            "title": "dedicated_fleet_offer.remove_wrap.title", // текст жирным
                            "minimal_value": null, // минимальное значение переменной
                            "cost": null, // стоимость услуги при текущем value
                            "type": "boolean", // тип переменной
                            "predicted_cost": null, // стоимость включения услуги, пока не используем, все пересчитанные значения или цены за километр/месяц.... пишем в cost
                            "id": "remove_wrap",
                            "maximal_value": null, // максимальное значение переменной
                            "group": "dedicated_fleet_offer.group.service" // новое поле группировки, позволяет объединить опции в группы
                        },
                        // опция заправки зависит от километров пробега, в итоговый счет включить не получиться, зато сможем отобразить стоимость услуги за километр 
                        {
                            "value": null,
                            "subtitle": "dedicated_fleet_offer.fueling.subtitle",
                            "default_value": false,
                            "unit": "рублей за километр",
                            "title": "dedicated_fleet_offer.fueling.title",
                            "minimal_value": null,
                            "cost": null,
                            "type": "boolean", // тип – radio button
                            "predicted_cost": null,
                            "id": "fueling",
                            "maximal_value": null,
                            "group": "dedicated_fleet_offer.group.service"
                        },
                        // опция мойки зависит от срока владения, стоимость масштабируется от времени владения, можно включить в итоговый счет
                        {
                            "value": null,
                            "subtitle": "dedicated_fleet_offer.washing.subtitle",
                            "default_value": false,
                            "unit": "рублей в месяц",
                            "title": "dedicated_fleet_offer.washing.title",
                            "minimal_value": null,
                            "cost": 10000,
                            "type": "boolean", // тип – radio button
                            "predicted_cost": null,
                            "id": "washing",
                            "maximal_value": null,
                            "group": "dedicated_fleet_offer.group.service"
                        }
                    ]
                },
                // массив сформированных предложений по каждой машине  
                "units_offers": [
                    {
                        "constructor_id": "simple_dedicated_fleet_unit_offer",
                        "is_corp_session": false,
                        "type": "dedicated_fleet_unit_offer",
                        "total_cost": 440000,
                        "device_id": "",
                        "holding_cost": 440000,
                        "behaviour_constructor_id": "simple_dedicated_fleet_unit_offer",
                        "deadline": 1646409312,
                        "name": "simple_dedicated_fleet_unit_offer",
                        "group_name": "",
                        "price_constructor_id": "simple_dedicated_fleet_unit_offer",
                        "offer_id": "5f4ad46a-2854-8099-317e-591641e02034",
                        "localizations": {},
                        "duration": 2667592000,
                        "is_plus_user": false,
                        "wallets": [],
                        // блок полностью повторяет unit_builder/secondary, после назначения машины слот можно редактировать, в этом случае выгодно хранить массив патчей 
                        // от исходной конфигурации, но не сейчас
                        "secondary": [
                            {
                                "value": null,
                                "subtitle": "dedicated_fleet_offer.remove_wrap.subtitle",
                                "default_value": false,
                                "unit": "",
                                "title": "dedicated_fleet_offer.remove_wrap.title",
                                "minimal_value": null,
                                "cost": 10000, // задаем через оффер билдер
                                "type": "boolean", // тип – radio button
                                "predicted_cost": null, 
                                "id": "remove_wrap",
                                "maximal_value": null,
                                "group": "dedicated_fleet_offer.group.service"
                            },
                            {
                                "value": null,
                                "subtitle": "dedicated_fleet_offer.fueling.subtitle",
                                "default_value": false,
                                "unit": "рублей километр",
                                "title": "dedicated_fleet_offer.fueling.title",
                                "minimal_value": null,
                                "cost": 7, // задаем через оффер билдер прибавку к стоимости за км
                                "type": "boolean", // тип – radio button
                                "predicted_cost": null,
                                "id": "fueling",
                                "maximal_value": null,
                                "group": "dedicated_fleet_offer.group.service"
                            }
                        ]
                    },
                    {
                        "constructor_id": "simple_dedicated_fleet_unit_offer",
                        "is_corp_session": false,
                        "type": "dedicated_fleet_unit_offer",
                        "total_cost": 440000,
                        "device_id": "",
                        "holding_cost": 440000,
                        "behaviour_constructor_id": "simple_dedicated_fleet_unit_offer",
                        "deadline": 1646409312,
                        "name": "simple_dedicated_fleet_unit_offer",
                        "group_name": "",
                        "price_constructor_id": "simple_dedicated_fleet_unit_offer",
                        "offer_id": "f8fa2e3a-75dd-e52a-2b65-315a2e88b1c3",
                        "localizations": {},
                        "duration": 2667592000,
                        "is_plus_user": false,
                        "wallets": [],
                        "secondary": [
                            {
                                "value": null,
                                "subtitle": "dedicated_fleet_offer.remove_wrap.subtitle",
                                "default_value": false,
                                "unit": "",
                                "title": "dedicated_fleet_offer.remove_wrap.title",
                                "minimal_value": null,
                                "cost": 10000, // задаем через оффер билдер
                                "type": "boolean", // тип – radio button
                                "predicted_cost": null,
                                "id": "remove_wrap",
                                "maximal_value": null,
                                "group": "dedicated_fleet_offer.group.service"
                            },
                            {
                                "value": null,
                                "subtitle": "dedicated_fleet_offer.fueling.subtitle",
                                "default_value": false,
                                "unit": "",
                                "title": "dedicated_fleet_offer.fueling.title",
                                "minimal_value": null,
                                "cost": 7, // задаем через оффер билдер прибавку к стоимости за км
                                "type": "boolean", // тип – radio button
                                "predicted_cost": null,
                                "id": "fueling",
                                "maximal_value": null,
                                "group": "dedicated_fleet_offer.group.service"
                            }
                        ]
                    }
                ],
                "tariff_plan": { // режим оплаты с возможными значениями
                    "values": [
                        {
                            "value": "tariff_1",
                            "title": "dedicated_fleet_offer.tariff_plan.tariff_1"
                        },
                        {
                            "value": "tariff_2",
                            "title": "dedicated_fleet_offer.tariff_plan.tariff_2"
                        },
                        {
                            "value": "tariff_3",
                            "title": "dedicated_fleet_offer.tariff_plan.tariff_3"
                        }
                    ],
                    "value": null,
                    "title": "dedicated_fleet_offer.tariff_plan.title",
                    "default_value": "tariff_1",
                    "id": "tariff_plan"
                },
                "is_plus_user": false,
                "total_cost": 1760000,
                "localizations": {},
                "constructor_id": "simple_dedicated_fleet_offer",
                "offer_id": "1d9bff71-c398-0592-97c7-ade9b6fe06e0",
                "wallets": [],
                "type": "dedicated_fleet_offer",
                "list_priority": 0,
                "behaviour_constructor_id": "simple_dedicated_fleet_offer",
                "prices": null,
                "is_corp_session": false,
                "payment_methods": [],
                "deadline": 1646409312
            }
        ],
        "property_patches": [],
        "models": {},
        "localizations": {},
        "transportation": {},
        "views": [],
        "defaults": {
            "account_id": "card"
        },
        "visibility": [],
        "cars": []
    }
}
```



