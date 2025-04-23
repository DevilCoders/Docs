## Добавление фильтров аудитории

Чтобы иметь возможность настраивать кампанию на разных пользователей через CRM, 
надо перенести в неё актуальные кварги экспериментов. Мы уменьшаем возможности инструмента экспериментов, которые можно будет использовать из CRM - 
переносим популярные кварги.
Расчёт на то, что это покроет самые популярные сценарии и упростит их.

На мой взгляд, для начала надо переносить кварги:
- часто используемые;
- кварги, которые хотят часто использовать; 
- кварги, которые легко будет настроить через CRM.

Настраивать через CRM можно будет выбором в чекбоксе, выбором из списка, добавлением в текстовое поле. 
Здесь решение за фронтенд-разработчиками.
Если кварг не получится настроить нажатием пары кнопок - на мой взгляд, нет смысла выносить его в CRM.

Здесь возможны такие варианты:
1. Собрать все кварги и захардкодить их в CRM. 
Плюсы - более дешёвая реализация со стороны бэкенда; каждый новый кварг будет обсуждаться с командой CRM.
Минусы - для каждого нового кварга надо будет подключать фронтенд-разработку, 
знания о кваргах продукта будут вынесены в CRM.
2. Создать в продуктовом сервисе `promotions` новую ручку, которая будет отдавать кварги, доступные для выбранного типа коммуникациии.
Плюсы и минусы обратны первому варианту. Также в эту ручку впоследствии можно будет добавить что-то кроме кваргов. 
Это может пригодиться для запусков кампаний по событию в продукте.
3. Добавить конфиг с кваргами, читать его в админке экспериментов, и для общих кваргов всех потребителей отрисовывать упрощённый интерфейс админки. 
В конфиге будет маппинг потребитель -> список кваргов с их описанием 
(тип настройки, элемент интерфейса в админке - чекбокс или что-то сложнее, тексты). Возможен как быстрый вариант до того, 
как CRM реализует интеграцию на своей стороне.
4. Реализовать логику, аналогичную предлагаемой для CRM, в нашей админке коммуникаций. 

**Можно пойти по такому пути**:
- для команды CRM делаем ручку с доступными кваргами;
- пока не готова реализация со стороны CRM - можно попробовать сделать упрощенный вид эксперимента в нашей админке коммуникаций Go.
План этого альтернативного варианта [здесь](audience_in_promotions_admin.md)

После выбора кваргов в админке они должны отправляться в `crm-admin`, оттуда - в `crm-hub`, а дальше - прокидываться в `promotions`. 

#### Какие кварги сейчас обычно используются в экспериментах фуллскринов
- location::position FALLS_INSIDE - самый популярный, почти в каждом фуллскрине (но непонятно, как задавать через CRM)
- application, platform, version
- phone_id (для сегментации)
- has_ya_plus
- has_plus_cashback
- plus_status (если аналогичен другим кваргам плюса - непонятно, зачем)
- zone

Более сложный пример существующей настройки: по тегу `churn_in_30d_now_not_in_plus` и кваргу `plus_status::string = "no_plus"`.

Будет интересно добавить point_a, point_b, zone выбором из списка, сурж.
*C добавлением точки A может возникнуть сложность, потому что её можно задать несколькими разными способами.*
Недавно в шорткаты был добавлен кварг новичка (показывает, были ли у пользователя заказы в сервисе).
Может быть интересно позже протащить его в другие типы коммуникаций и добавить в CRM.

#### Возможная схема ручки, возвращающей поддержанные фильтры

Так как продуктовые планы могут меняться, а фильтры - добавляться или терять актуальность, 
можно попробовать возвращать их так, чтобы было легко что-то добавить или убрать.

Можно начать с таких типов фильтров:
- выбор да/нет, опциональный (`boolean`)
- строковое текстовое поле (`string`)
- выбор из списка (`string` и список возможных вариантов)
- число (`number`)

Ручку добавим в новом сервисе `communication-audience`

```
/communications-audience/v1/available-filters:
    get:
        summary: 'Returns available filters for given promotion type'
        operationId: PromotionFilters
        parameters:
          - name: promotion_type
            in: query
            type: string
            enum:
              - fullscreen
              - story
              - deeplink_shortcut
              - object_on_map
            required: true
        responses:
            '200':
                description: OK
                schema:
                    $ref: '#/definitions/AvailableFiltersResponse'
            '404':
                description: Not found

definitions:
    TypedFilter:
        type: object
        additionalProperties: false
        properties:
            label:
                type: string
                description: текст для названия фльтра в CRM
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
            function_type:
                type: string
                description: | 
                    функция фильтра. Например, разбиение по пользователям (phone_id), 
                    устройствам (android) или состоянию приложения (геозона, наличие Плюса)
                enum: 
                  - user
                  - device
                  - application_state
            supports_alternatives:
                type: bool
                description: | 
                    можно предложить задать несколько значений. 
                    При настройке коммуникации заданные значения фильтров будут связаны как ИЛИ
                default: false
        required:
          - label
          - filter_id
          - value_type
          - function_type

    TypedFilterWithChoiceOptions:
        type: object
        additionalProperties: false
        properties:
            label:
                type: string
                description: текст для названия фильтра в CRM
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
                  - string
                  - number
            function_type:
                type: string
                description: | 
                    функция фильтра. Например, разбиение по пользователям (phone_id), 
                    устройствам (android) или состоянию приложения (геозона, наличие Плюса)
                enum: 
                  - user
                  - device
                  - application_state
            available_choices:
                type: array
                description: доступные варианты выбора значения фильтра
                items: 
                    oneOf:
                      - type: string
                      - type: number
            supports_alternatives:
                type: bool
                description: | 
                    можно предложить задать несколько значений. 
                    При настройке коммуникации заданные значения фильтров будут связаны как ИЛИ
                default: false
        required:
          - label
          - filter_id
          - value_type
          - function_type
          - available_choices
    
    AvailableFiltersResponse:
        type: object
        additionalProperties: false
        properties:
            filters:
                type: array
                items:
                    anyOf:
                      - $ref: '#/definitions/TypedFilter'
                      - $ref: '#/definitions/TypedFilterWithChoiceOptions'
        required:
          - filters
```

При реализации можно брать пересечение кваргов из конфига по потребителям для потребителей, 
относящихся к типу коммуникации.

#### Возможная схема конфига с кваргами
```
description: |
    Настройки упрощённого интерфейса админки экспериментов.
    Схема: exp3_consumer -> communication_settings
default: {}
maintainers:
  - sia-raimu
tags: [notfallback]
schema:
    type: object
    additionalProperties:
        $ref: '#/definitions/CommunicationSettings'
    definitions:
        CheckBox:
            type: object
            additionalProperties: false
            properties:
                 tanker_key:
                    description: ключ для отображения названия настройки в админке
                    type: string
            required:
              - tanker_key

        CommunicationSettingUi:
            type: object
            additionalProperties: false
            properties:
                ui_element:
                    oneOf:
                      - $ref: "#/definitions/CheckBox"
            required:
              - ui_element

        CommunicationSetting:
            type: object
            additionalProperties: false
            properties:
                setting_type:
                    description: тип настройки, например, кварг или тег
                    type: string
                    enum:
                      - exp3_kwarg
                ui:
                    $ref: "#/definitions/CommunicationSettingUi"
            required:
              - setting_type
              - ui

        CommunicationSettings:
            settings:
                type: array
                items:
                    $ref: "#/definitions/CommunicationSetting"
            required:
              - settings
```

Также можно здесь задавать не вид элемента, а только их типы, по аналогии с предложенным api ручки.
Финально определиться лучше после обсуждений с разработчиками экспериментов.
