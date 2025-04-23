## Интеграция пользовательских коммуникаций с CRM

В рамках переосмысления интеграции можно пойти по пути `feeds-admin` и `driver-wall` 
и предложить новую ручку пользовательских коммуникаций, поддерживающую массовую публикацию коммуникаций.

#### Что можно позаимствовать из этих сервисов:

- api ручки в запросе принимает параметры, по которым можно настраивать аудиторию, а не эксперимент. 
Способ настройки определяется внутри сервиса (так можно отойти от настройки экспериментом);
- ручку можно вызывать несколько раз, передавая ей такое количество коммуникаций, которое сервис способен обработать за раз.

#### Изменения в api

Сейчас ручка публикации фуллскринов выглядит так:

```
/admin/promotions/publish/:
    post:
        summary: 'Publish promotion with given id'
        operationId: AdminPublish
        parameters:
          - in: body
            name: body
            description: PublishRequest
            required: true
            schema:
                $ref: '#/definitions/AdminPublishRequest'
        responses:
            '200':
                description: OK
                schema:
                    $ref: 'promotions/definitions.yaml#/definitions/EmptyResponse'
            '400':
                description: OK
                schema:
                    $ref: 'promotions/definitions.yaml#/definitions/ErrorResponse'
            '409':
                description: Conflict
                schema:
                    $ref: 'promotions/definitions.yaml#/definitions/ErrorResponse'
            '502':
                description: Bad Gateway
                schema:
                    $ref: 'promotions/definitions.yaml#/definitions/ErrorResponse'

definitions:
    AdminPublishRequest:
        type: object
        properties:
            promotion_id:
                type: string
            experiment:
                type: string
            yql_link:
                description: |
                    Не актуально для промо-объектов на карте,
                    т.к. для них не поддержана публикация по YQL.
                type: string
            start_date:
                type: string
            end_date:
                type: string
            ticket:
                description: |
                    Не актуально для промо-объектов на карте.
                    Используется только в feeds-admin.
                type: string
        required:
          - promotion_id
          - start_date
          - end_date
          - ticket
        additionalProperties: false
```

Можно предложить похожее api, но с возможностью публикации по фильтрам и на пользователей. 

Новую ручку для CRM можно предложить в новом сервисе `communication-audience`.
Она будет примерно такой:

```
/communications-audience/v1/publish:
    post:
        description: |
            Ручка, публикующая коммуникации на пассажиров.
            Умеет задавать аудиторию коммуникации тремя способами:
                1) Списком идентификаторов пользователя
                2) Фильтрами
                3) Фильтрами и списком идентификаторов пользователя
            Для задания аудитории этими способами нужно сделать следующее:
                1) Задать только персональные коммуникации и списки пользователей внутри
                2) Задать только фильтры
                3) Задать и персональные коммуникации, и фильтры. 
                Тогда персональные коммуникации опубликуются на указанных пользователей с учётом заданных фильтров, 
                а общая коммуникация communication - только с учётом фильтров
        parameters:
          - in: header
            name: X-Idempotency-Token
            description: |
                токен идемпотентности запроса
            type: string
            required: false
            minLength: 1
            maxLength: 64
          - in: body
            name: body
            schema:
                type: object
                additionalProperties: false
                required:
                  - id
                  - communication
                  - campaign_label
                properties:
                    id:
                        description: ID запроса.
                        type: string
                    personal_communications:
                        description: |
                            Коммуникации, настроенные на конкретного пользователя или список пользователей.
                        type: array
                        maxItems: 100
                        items:
                            $ref: '#/definitions/PersonalCommunication'
                    communication:
                        description: коммуникация, которая будет отправлена всем при настройке фильтрами
                        $ref: '#/definitions/Communication'
                    campaign_label:
                        description: | 
                            Метка кампании. Будет использоваться для определения и сохранения кампании
                            и логирования во всех сервисах, участвующих в публикации
                        type: string
                    filters:
                        description: фильтры для настройки аудитории
                        $ref: '#/definitions/Filters'
                    is_test_publication:
                        description: |
                            Cообщает, что публикация является тестовой.
                            Тестовая публикация сможет показываться на устройстве больше одного раза.
                        default: false
        responses:
            '200':
                description: OK
                schema:
                    type: object
                    additionalProperties: false
                    properties:
                        id:
                            type: string
                            description: Значение, переданное в поле id в запросе
                        audience_info:
                            type: array
                            description: список данных о разметке аудитории в результате запроса
                            items: 
                                $ref: '#/definitions/Audience'
                    required:
                      - id
                      - audience_info
            '409':
                description: Conflict
            '500':
                description: Internal error

definitions:
    Communication:
        properties:
            type: object
            additionalProperties: false
            communication_id:
                type: string
            start_date:
                type: string
            end_date:
                type: string
            ticket:
                description: |
                    Не актуально для промо-объектов на карте.
                    Используется только в feeds-admin.
                type: string

    User:
        type: object
        description: объект для идентификаторов, определяющих пользователя
        additionalProperties: false
        properties:
            id_type:
                type: string
                enum:
                  - yandex_uid
                  - phone_id
                  - personal_phone_id
                  - device_id
            id: 
                type: string
                description: | 
                    Один из идентификаторов пользователя.
                    Ожидается, что есть смысл заводить кампанию только по одному идентификатору, 
                    поэтому api явно ограничивает количество идентификаторов

    Audience:
        type: object
        description: информация о разметке аудитории
        additionalProperties: false
        properties:
            communication_id: 
                type: string
                description: идентификатор коммуникации
            audience_label:
                type: string
                description: метка аудитории
        required:
          - communication_id
          - audience_label

    PersonalCommunication:
        type: object
            additionalProperties: false
            users: 
                type: array
                maxItems: 1000
                items:
                    $ref: '#/definitions/User'
            communication_id:
                type: string
            start_date:
                type: string
            end_date:
                type: string
            ticket:
                description: |
                    Не актуально для промо-объектов на карте.
                    Используется только в feeds-admin.
                type: string
            required:
              - users

    TypedFilter:
        type: object
        additionalProperties: false
        properties:
            filter_id:
                type: string
                description: | 
                    идентификатор фильтра. Нужен, чтобы использовать в конфигах, 
                    экспериментах, для определения типа фильтра.
                    Поэтому не должен меняться
            value_type:
                type: string
                description: тип значения фильтра
                enum:
                  - boolean
                  - string
                  - number
            value:
                oneOf:
                  - type: boolean
                  - type: string
                  - type: number
                description: выбранное значение
        required:
          - filter_id
          - value_type
          - value

    TypedFilterWithAlternatives:
        type: object
        additionalProperties: false
        properties:
            filter_id:
                type: string
                description: | 
                    идентификатор фильтра. Нужен, чтобы использовать в конфигах, 
                    экспериментах, для определения типа фильтра.
                    Поэтому не должен меняться
            value_type:
                type: string
                description: тип значения фильтра
                enum:
                  - boolean
                  - string
                  - number
            values:
                items:
                    oneOf:
                      - type: boolean
                      - type: string
                      - type: number
                description: выбранные значения, если есть
        required:
          - filter_id
          - value_type
          - values

    Filters:
        type: object
        additionalProperties: false
        properties:
            filters:
                type: array
                items:
                    anyOf:
                      - $ref: '#/definitions/TypedFilter'
                      - $ref: '#/definitions/TypedFilterWithAlternatives'
        required:
          - filters
```

### Реализация

На первом этапе можно переиспользовать код ручки  `/admin/promotions/publish/`.

Как может быть размечена аудитория:
1. Только по идентификаторам пользователей. Размечаем метками, про них ниже.
2. По идентификаторам пользователей и фильтрам. Размечаем метками, эксперимент связываем с меткой, фильтры добавляем в эксперимент позже, в сервисе аудитории.
3. Только по фильтрам. Здесь оставляем логику, как было раньше.

У новой ручки две задачи: сохранить коммуникацию внутри promotions и сохранить разметку аудитории. 

1. Сохранение коммуникации. Переиспользуем существующую базу `promotions` и существующий кэш коммуникаций. 
Для того, чтобы позже правильно разметить аудиторию, за каждой коммуникацией будет закреплёна метка.
(можно придумать другую терминологию, чтобы не путать с тегами сервиса тегов). В базе `promotions` добавится новое поле 
для списка меток коммуникации. Возможно, метки стоит вернуть CRM в ответе ручки (например, если они пригодятся для аналитики). 

Также добавится новая таблица, в которой будет храниться связь метки с временем публикации и экспериментом, в котором будут настроены фильтры. 

| audience_label  | starts_at | ends_at   | published_at | experiment_name |
| --------------- |-----------|-----------|--------------|-----------------|
| "campaign12345" | timestamp | timestamp | timestamp    | "12345exp"      |


Теперь время для коммуникаций, содержащих метки, будет связано с меткой, 
а не с самой коммуникацией, а для одной коммуникации может быть доступно несколько меток, 
так что время для новых коммуникаций в таблицу коммуникаций сохранять не следует. Время публикации теперь тоже стоит связать с меткой. 

Поля, относящиеся к публикации, имеет смысл сохранять в эту новую таблицу, а поля, относящиеся к виду коммуникации - в `promotions.promotions`.

2. Сохранение аудитории. Аудитория будет сохраняться в новом хранилище. Считаю, что правильно работу с аудиторией 
инкапсулировать в новом сервисе. 
Поэтому добавится поход в этот сервис с меткой коммуникации и либо фильтрами, либо идентификаторами пользователей. 
У сервиса будет отдельно запрос на разметку и запрос статуса разметки, здесь только зовём ручку разметки. 
