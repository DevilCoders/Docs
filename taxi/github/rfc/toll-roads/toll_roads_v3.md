# Изменения для фичи "Платные Дороги" (Toll Roads)

## Цели

- разграничить доступность платных дорог для разных тарифов. Сделать так что бы для некоторых тарифов платные дороги не были доступны вовсе, не зависимо от того как проходит маршрут (например для тарифа Курьер), а для каких то тарифов предлагались только есть точки А и Б находятся на платной дороге и по другому туда не прихать.

- поддержать новый UI выбора платных дорог [дизайн] (https://www.figma.com/file/HqiJ8t81poeL4dYL2pDM3xqL/Платные-дороги?node-id=2860%3A12326)

- не платные дороги для ЦКАД, т.к. мы не знаем сколько стоит проезд и пассажир не может ее оплатить. Поэтому не предлагаем платную дорогу. Если точки А и Б на ЦКАД, то показываем общий текст.

- перенести логику управления показом платных дорог на бекенд

- вынести логику формирования текстов на бекенд

## Решение

### Вынесение логики платных дорог на бекенд

Предлагается перенести всю логику управления платными дорогами на бекенд. Правильным местом где должны быть знания о платности будет /routestats.

Отказываемся от признака toll_roads_enabled в /zoneinfo для конкретного тарифа, т.к. мы не можем его контролировать для конкретных маршрутов и точек А и Б.

Для этого клиент будет как и раньше запрашивать у MapKit платную и бесплатную дорогу, но до ответа /routestats показывать только бесплатную дорогу (если есть только платный вариант, то платную). Когда /routestats ответит, тогда исходя из ответа клиент будет рисовать платную дорогу на карте.

В первой версии бекенд всегда присылает плашку и клиент ее определяет есть ли платная дорога на основании ответа MapKit + /routestats. В будущем когда бек научится присылать сразу две цены для обеих дорог, тогда будем ориентироваться только на /routestats.

Для этого предлагается в ответ /routestats добавить:

```yaml
required:
    - toll_roads
    
toll_roads:
    $ref: '#/definitions/TollRoads'
                    
definitions:
    TollRoads:
        type: object
        required:
            - available
            - has_tolls
        properties:
            has_tolls:
                type: boolean
            available:
                type: string
                enum:
                    - enabled
                    - disabled
                    - enabled_if_only_tolls
```
enabled - платная дорога доступна
disabled - платная дорога не доступна
enabled_if_only_tolls - платная дорога доступна только если это единственный маршурт (для варианта когда точки А и Б на платной дороге)

Поле has_tolls оставляем, это признак того посчитан ли оффер по платной дороге или нет.

Убираем поле auto_payment, т.к. бекенд теперь сам формирует тексты.

Поскольку платные дороги не умеют работать с альтпинами, то бекенд не должен присылать альтпины если есть платная дорога.

Для того, что бы новый /routestats поддержал эти изменения клиент будет передавать в уже существующем блоке supported (который лежит в корне запроса) объект с type: toll_roads_v2. Ниже привожу схему этого блока:


```yaml
definitions:
    SupportedPayload:
        type: object
        additionalProperties: false
        properties:
            classes:
                type: array
                x-taxi-cpp-type: std::set
                items:
                    type: string

    SupportedItem:
        type: object
        additionalProperties: false
        required:
          - type
        properties:
            type:
                type: string
            payload:
                $ref: '#/definitions/SupportedPayload'

requestBody:
    type: object
    additionalProperties: false
    required:
        - supported
    # тут какие-то ещё поля
    properties:
        supported:
            description: список поддержанных опций
            type: array
            items:
                $ref: "#/definitions/SupportedItem"
        
```

Пример supported с нашим флагом:
```json
{
    "supported": [
        {
            "type": "toll_roads_v2"
        }
    ]
}
```

### ЦКАД

Введя такой ответ бекенде зная точки А и Б сможет управять доступность платных дорог для конкретных маршрутов - не предлагать платные дороге через ЦКАД. 

## Шереметьево

Для Шереметьево надо присылать отдельные тексты.

Так как оплата проездка происходит на пункте оплаты, то цена поездки зависит от выбранного способа оплаты. Если выбран безналичный способ оплаты, то цена проезда по платной дороге включена в стоимость offer, если выбраны наличные, то пользователь сам оплачивает проезд на пунке проезда.

Логика для UI отображения на саммари: в случае если пользователь выбрал платную дорогу и потом поменял способ оплаты, мы должны показать ему алерт, который бы мы ему показали если бы он снова выбрал платную дорогу. Это нужно для того, что бы пользователь увидел как он будет оплачивать дорогу.

Так алерт надо показывать только при переключении с начлиного на безналичный способ оплаты и наоборот. В случае если пользователь меняет способ оплаты в меню, тогда показываем алерт при его заходе на саммари (ответе /routestats).

Тексты будут приходить в UIOnSummary.select_action

### Тексты и UI

Предлагается что бы теперь сам бекенд определял текст и тот UI которые должен быть использован в том или ином случае. Для этого обогатим модель toll_roads типом UI и текстами.

```yaml
required:
    - toll_roads
    
toll_roads:
    $ref: '#/definitions/TollRoads'

definitions:
    TollRoads:
        type: object
        required:
            - available
            - has_tolls            
        properties:
            has_tolls:
                type: boolean
            available:
                type: string
                enum:
                    - enabled
                    - disabled
                    - enabled_if_only_tolls
            hint_on_map:
                type: object
                properties:
                    text:
                        type: string

                    icon_tag:
                        type: string
            ui:
                oneOf:
                    - $ref: '#definitions/UIOnSummary'
                    - $ref: '#definitions/UIOnOrderButton'                    
    UIOnSummary:
        type: object
        required:
            - title
            - subtitle 
            - cost_type           
        properties:
            title:
                type: string
            subtitle:
                type: string
            cost_type:
                $ref: '#/definitions/CostType'
            select_action:
                type: object
                required:
                    - title
                    - button_text
                properites:
                    title:
                        type: string
                    attributed_text:
                        type: 
                            $ref: #definitions/attributed_string
                        description: https://github.yandex-team.ru/taxi/rfc/blob/3ed22067cbef78de67fa8954b972bbd536ce64bf/layers/attributed_text.md
                    button_text:
                        type: string
    
    UIOnOrderButton:
        type: object
        # Для кейса, когда доступна только одна платная дорога
        # в версии ui на кнопке заказать, нам не нужно будет отображать
        # чекбоксы выбора платной/бесплатной, поэтому они опциональны.
        # Также опционален button_subtitle для большей гибкости, чтоб
        # не слать в нём пустую строку, если он не нужен
        required:
            - title
            - text
            - cost_type
            - button_text
        properties:
            title:
                type: string
            text:
                type: string
            cost_type:
                $ref: '#/definitions/CostType'
            free_road_text:
                type: string
            toll_road_text:
                type: string                
            button_text:            
                type: string
            button_subtitle:
                type: string

    CostType:
        type: string
        description: |
            Тип цены, которая содержится в текстах. Нужно при логгировании
            событий, чтобы различать разные показанные пользователю тексты
        enum:
          - unknown  # Информация о цене отсутствует
          - approx   # Указана примерная цена или диапазон
          - exact    # Указана точная цена
        
```

Теперь все тексты формирует сам бекенд. В том числе и цены, клиент просто применяет currency_rules к необходимым полям ответа.

Также для аналитики в объекты ui добавлено поле cost_type, при помощи которого можно будет создавать разные события в зависимости от того, содержится ли цена в тексте и насколько точная. В новой версии логики клиенты ничего не знают о содержимом текстов, поэтому был добавлен этот параметр в ответ бэка.

Для ui_on_summary, если не пришел select_action, то мы не показываем окно при выборе платной дороги.

При этом блок ui должен быть обязательным в случае если платная дорога доступна. 

### Ограничение для тарифа

Каждый тариф на своем уровне может переопределить модель toll_roads и сделать платную дорогу видимой / не видимой.
Для этого на уревне service_levels будет приходить модель override_toll_roads, которые позволят переопределять поведение полей из корневого ответа. Так же это позволить переопределить UI для любого из тарифов.


```yaml
required:
    - toll_roads
    
toll_roads:
    $ref: '#/definitions/TollRoads'        

service_levels:
    type: array
    items:
        // ...
        override_toll_roads:
            type: object:
            properties:
                available:
                    type: string
                    enum:
                        - enabled
                        - disabled
                        - enabled_if_only_tolls
                hint_on_map:
                    type: object
                    properties:
                        text:
                            type: string

                        icon_tag:
                            type: string
                ui:
                    oneOf:
                        - $ref: '#definitions/UIOnSummary'
                        - $ref: '#definitions/UIOnOrderButton'                   
}
```

### Самый быстрый тариф и Alternatives

В случае если у нас есть alternatives, то, и структура override_toll_roads переопределена на уровне service_levels.override_toll_roads, тогда она так же должна быть переопределена на уровне alternatives.service_levels.override_toll_roads, что бы клиенту не приходилось мержить service_level из alternatives с теми что лежат в корне.

Сейчас самый быстрый тариф приходит в alternatives с типом multiclass. В случае если есть вертикали, в рамках вертикали так же может быть multiclass и он сейчас мержится с тем, что лежит на уровне alternatives. Тоесть есть возможность переопределения override_toll_roads в verticals.multiclass. 

Для самого быстрого тарифа бек присылает структуру override_toll_roads в корне alternative, т.к. она не имеет смысла на уровне serive_level. Бек решает сам, доступна ли платная дорога в зависимости от тарифов которые есть в самом быстром тарифе, а так же может переопределить это в рамках конкретной вертикали. 

Если в тарифах есть хотя бы один, где по платной дороге ехать нельзя, а на остальных можно, то блокировать кнопку заказать и писать на ней что платная самый быстрый не работает с платными дорогами. Иначе клиенту не понятно где цена по платке включена в стоимсть, где нет, и где вообще есть платная дорога.

В первой итерации: клиенты дополнительно валидирут флаг доступности из override_toll_roads с MapKit.

Пример alternatives 

```json
alternatives": {
        "options": [{
            "details": {
                "description": "Будем искать машину в нескольких тарифах сразу. Приедет ближайшая.",
                "estimated_waiting": {
                    "message": "44 мин",
                    "seconds": 2640
                },
                "order_button": {
                    "enabled": false,
                    "text": "Выберите минимум два тарифа"
                },
                "price": "от 0 $SIGN$$CURRENCY$",
                "search_screen": {
                    "subtitle": "в нескольких тарифах",
                    "title": "Поиск"
                }
            },
            "distance": "33 км",
            "multiclass_popup": {
                "show_conditions": [{
                    "count": 3,
                    "metric": "tariff_switch",
                    "period_seconds": 8
                }],
                "show_count": 3,
                "text": "Самый\nбыстрый"
            },
            "name": "Самый быстрый",
            "offer": "c817d939db9347b99b80b9786292ed0c",
            "selection_rules": {
                "min_selected_count": {
                    "text": "Выберите минимум два тарифа",
                    "value": 2
                }
            },
            "selector": {
                "icon": {
                    "size_hint": 300,
                    "url": "https://tc.tst.mobile.yandex.net/static/test-images/1138/7a5eba0b595d42c2856cd1a7bcf5eac9",
                    "url_parts": {
                        "key": "TC",
                        "path": "/static/test-images/1138/7a5eba0b595d42c2856cd1a7bcf5eac9"
                    }
                }
            },
            "service_levels": [{
                "class": "econom",
                "selected": false
            }, {
                "class": "business",
                "selected": false
            }, {
                "class": "vip",
                "selected": false
            }],
            "override_toll_roads": {
                "available": "enabled"
            }
            "time": "50 мин",
            "time_seconds": 3000,
            "type": "multiclass"
        }]
    },
```

### Итоговый YML

/routestats

Запроc

```yaml
parameters:
    type: object
    required:
        - supported
    properties:
        supported:
            type: array
            items:
                type: string
                enum:
                    - toll_roads_v2        
```

Ответ

```yaml
required:
    - toll_roads
    
toll_roads:
    $ref: '#/definitions/TollRoads'     
            
            
service_levels:
    type: array
    items:
        // ...
        toll_roads:
            $ref: '#/definitions/TollRoads'

definitions:
    TollRoads:
        type: object
        required:
            - available
            - has_tolls
        properties:
            has_tolls:
                type: boolean
            available:
                type: string
                enum:
                    - enabled
                    - disabled
                    - enabled_if_only_tolls
            hint_on_map:
                type: object
                properties:
                    text:
                        type: string

                    icon_tag:
                        type: string

            ui:
                oneOf:
                    - $ref: '#definitions/UIOnSummary'
                    - $ref: '#definitions/UIOnOrderButton'                    
    UIOnSummary:
        type: object
        required:
            - type
            - title
            - subtitle
            - cost_type       
        properties:
            type:
                type: string
                enum:
                    - on_summary
            title:
                type: string
            subtitle:
                type: string
            cost_type:
                $ref: '#/definitions/CostType'
            select_action:
                type: object
                required:
                    - title
                    - button_text
                properites:
                    title:
                        type: string
                    attributed_text:
                        type: 
                            $ref: #definitions/attributed_string
                    button_text:
                        type: string
    
    UIOnOrderButton:
        type: object
        required:
            - type
            - title
            - text
            - cost_type
            - button_text
        properties:
            type:
                type: string
                enum:
                    - on_order_button                
            title:
                type: string
            text:
                type: string
            cost_type:
                $ref: '#/definitions/CostType'
            free_road_text:
                type: string
            toll_road_text:
                type: string                
            button_text:            
                type: string
            button_subtitle:
                type: string

    CostType:
        type: string
        description: |
            Тип цены, которая содержится в текстах. Нужно при логгировании
            событий, чтобы различать разные показанные пользователю тексты
        enum:
          - unknown  # Информация о цене отсутствует
          - approx   # Указана примерная цена или диапазон
          - exact    # Указана точная цена
        
```

Пример ответа routestats

```json
{
    // ...
    "toll_roads": {
        "has_tolls": false,
        "available": "enabled",
        "hint_on_map": {
            "text": "Поехать по платной дороге +250₽",
            "icon_tag": "coins"
        },
        "ui": {
            "type": "on_summry",
            "title": "По платной быстрее на 15 мин",
            "subtitle": "Стоит 250₽",
            "cost_type": "exact",
            "select_action": {
                "title": "Проезд по платной дороге до Шереметьево входит в цену поездки",
                "button_text": "Хорошо"
            }
        }
    },
    "service_levels": [
        // ...    
        {
            "class": "express",
            "name": "Delivery",
            // ...
            "override_toll_roads": {
                "available": "enabled_if_only_tolls",
                "ui": {
                    "type": "on_summary",
                    "title": "Водитель может ехать только по платной дороге",
                    "cost_type": "unknown",
                    "subtitle": "Вам придется что-то доплатить водителю"
                }
            },
        },
        {
            "class": "courier",
            "name": "Courier",
            // ...
            "override_toll_roads": {
                "available": "disabled"
            },
        },                       
    ]
}
```

## В поездке

Для отображения на экране поездке расширяем блок toll_roads в ручке /taxiontheway что бы отображать информацию о платной дороге. Уберем старые поля auto_payment и price, т.к. теперь бекенд сам будет присылать нам готовые тексты.

Бекенд всегда присылает блок has_toll_road, даже если клиент его не отправлял при создани заказа - на основании этого флага, клинт будет строить маршрут в поездке (раньше мы это делали из эксперимента). 

В случае если флаг не пришел, клиент считает что надо использовать бесплатную дорогу.

Для того, что бы новый /taxiontheway поддержал эти изменения клиент в запрос будет передавать в запрос массив supported и в него класть признак toll_roads_v2. 

Таким образом /taxiontheway будет выглядеть так (определение SupportedItem выше)

Запрос

```yaml
parameters:
    type: object
    required:
        - supported
    properties:
        supported:
            description: список поддержанных опций
            type: array
            items:
                type: string
                enum:
                    - toll_roads_v2
                    - ...        
```

Ответ


```yml
toll_roads:
    type: object
    required:
        - has_toll_road
    properties:
        has_toll_road:
            type: boolean
        ui:
            type: object
            required:
                - card
                - alert
            properties:
                card:
                    type: object
                    required:
                        - title
                    properties:
                        icon_tag:
                            type: string
                        title:
                            type: string
                        subtitle
                            type: string
                alert:                
                    type: object
                    required:
                        - title
                        - button_text
                    properites:
                        icon_tag:
                            type: string
                        title:
                            type: string
                        attributed_text:
                            type: 
                                $ref: #definitions/attributed_string
                        button_text:
                            type: string
```

Пример ответа:

```json
"toll_roads": {
    "has_toll_road": true,
    "ui": {
        "card": {
            "icon_tag": "rub_coins",
            "title": "По платной дороге",
            "subtitle": "Оплата дополнительно на пункте"
        },
        "alert": {
            "icon_tag": "rub_coins",
            "title": "Платная дорога оплачивается отдельно",
            "button_text": "Понятно"
        }
    }
}
```

## Расширение в будущем

В будудем необходимо добавить сразу цену платной дороги в алтернативу, что бы мы сразу знали время и цену.
Так же это позволит сразу присылать тексты, которые будут необходимы продуктово (например: на 15 минут быстрее).

## Особенности

Перестаем показывать платные дороги до ответа /routestats. В случае если /routestats не отвечает, то мы пользователю не предложим платную дорогу. 

## Вопросы и ответы

- просмотреть кейсы из [вики](https://wiki.yandex-team.ru/users/roman-nevr/kejjsy-platnyx-dorog/) и понять какие из них остануться, многие мы должны порешать


