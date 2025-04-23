## Задача

Необходимо поддержать мультикласс ("Самый быстрый") в вертикалях. 
Сейчас в вертикалях есть минимальная поддержка мультикласса - он создаётся для одной вертикали.
Надо добавить возможность создания своего мультикласса в каждой вертикали.
Можно считать, что пока запускается вариант вертикалей с селектором, поэтому добавлять мультикласс имеет смысл для него.

## Как сейчас устроен мультикласс

Мультикласс настраивается конфигами. 
Помимо конфигов-переключателей, есть такие конфиги:
 - `MULTICLASS_POPUP_SHOW_RULES` c правилами показа нотификации о мультиклассе в саммари - 
 неактуально, можно выпиливать;
 - `MULTICLASS_SELECTOR_ICON` для задания иконки в карточке мультикласса;
- `MULTICLASS_TARIFFS_BY_ZONE` - конфиг со списком тарифов;
- `MULTICLASS_DEFAULT_ENABLED` - конфиг-переключатель, значение которого прокидывается на клиент в `can_be_default`. 
 Определяет, может ли мультикласс показываться на главном экране.

В `/zoneinfo` на клиент возвращаются настройки мультикласса, полученные из конфига.
Дальше на клиенте сначала (и до получения ответа `/routestats`) строится мультикласс на основе этих настроек.
В самом `/routestats` список тарифов мультикласса перед возвращением на клиент отправляется в объект `MulticlassDirector`, 
где тарифы, которые не надо показывать, убираются из мультикласса.

В `/routestats` мультикласс возвращается в `alternatives`.
Структура мультикласса в `/routestats` содержит список тарифов, иконку селектора, 
необходимые тексты заголовков, информацию, полученную в `/routestats` (например, цена, eta).

Позиция мультикласса управляется экспериментом `summary_multiclass_tariff_position`.

Пока что имеющиеся конфиги и эксперименты останутся, потому что новый мультикласс в селекторе 
будет включаться экспериментом, и где-то пока потребуется старый мультикласс (и старая логика).

## Как сейчас реализован мультикласс в селекторе

Сейчас мультикласс можно добавить только в одну вертикаль в селекторе.
Настройки этой вертикали задаются в эксперименте `verticals_selector` в поле `multiclass` для той вертикали, 
для которой будет добавлен селектор, и содержат позицию мультикласса внутри вертикали 
и списка тарифов.

Для вертикалей позиция отдаётся в структуре вертикалей (поле `position`) в ответе `/zoneinfo`.

## Необходимые изменения

Нужно возвращать на клиент информацию о мультиклассе для каждой вертикали. 
Должна быть возможность конфигурировать тарифы в вертикали, тексты для разных экранов работы с мультиклассом, 
иконку селектора мультикласса, позицию в вертикали.

Также в дизайне карточки мультикласса появились заголовок и подзаголовок, которых не было раньше.
Можно сразу предусмотреть поля для них.

[Дизайн карточки в Figma](https://www.figma.com/file/OmooncuMjX6xkcxCeMB1Vh/Воронка-такси:-дерево-экспериментов?node-id=2520:55574)

## Решение

### Конфигурация мультикласса в вертикалях через эксперимент

Можно расширить схему эксперимента `verticals_selector`, добавив необходимые поля в объект мультикласса.
Теперь этот объект будет добавляться для каждой вертикали. 
Помимо списка тарифов и положения в вертикали, нужно предусмотреть поля для иконки и текстов.

```
multiclass:
    type: object
    additionalProperties: false
    required:
        - tariffs
        - default_enabled
    properties:
        position:
            type: integer
            description: |
                позиция "самого быстрого" внутри вертикали
                отсутствие параметра position означает, что
                multiclass нужно поставить в конце тарифов
        tariffs:
            type: array
            description: тарифы, которые нужно показать в "самом быстром" внутри
                данной вертикали
            items:
                type: string
        selector_icon:
            type: string
            description: image tag иконки в карточке мультикласса
        ### возможно, на первом этапе не будет необходимости конфигурировать тексты 
        ### экспериментом, будет достаточно захардкодить танкерные ключи
        texts:
            type: object
            additionalProperties: false
            properties:
                name:
                    type: string
                    example: "Самый быстрый"
                description_title:
                    type: string
                    example: "Несколько тарифов"
                description_subtitle:    
                    type: string
                    example: "Назначим ближайшую к вам машину"
        default_enabled:
                    type: boolean
                    description: |
                        Замена конфигу MULTICLASS_DEFAULT_ENABLED.
                        Определяет, может ли мультикласс показываться на главном экране.
                        Значение прокидывается на клиент в can_be_default                    
```

Тексты "Выберите минимум два тарифа" и "Поиск в нескольких тарифах" вряд ли будут изменяться.
Для остальных можно предусмотреть возможность изменять текст через эксперимент, но оставить эти поля опциональными, 
а в коде зашить дефолтные ключи.

### Возвращение настроек мультикласса в `/zoneinfo`

В `/zoneinfo`в структуру вертикалей уже были добавлены поля для одного "Самого быстрого" - 
на клиент возвращаются список тарифов и позиция в вертикали. 
Остальное бралось из поля `multiclass` в ответе. 
Теперь необходимо то, что может меняться для разных "Самых быстрых" на этапе вызова `/zoneinfo`, тоже перенести внутрь структуры вертикалей.
В структуру мультикласса в вертикали добавится иконка селектора и некоторые переводы.

```
GroupVertical:
    description: описание вертикали с типом group
    type: object
    additionalProperties: false
    required:
      - type
      - id
      - title
      - tariffs
      - default_tariff
      - can_make_order_from_summary
    properties:
        ...
        multiclass:
            description: описание "Самого быстрого" для вертикали
            items:
                $ref: "#/definitions/VerticalMulticlass"

VerticalMulticlass:
    type: object
    additionalProperties: false
    required:
      - tariffs
    properties:
        tariffs:
            description: список тарифов внутри "Самого быстрого"
            type: array
            items:
                type: string
        position:
            description: позиция "Самого быстрого" в вертикали
            type: integer
        selector_icon:
            description: иконка в карточке "Самого быстрого"
            $ref: definitions.yaml#/definitions/image
        can_be_default:
            description: может ли мультикласс быть показан на главном экране
            type: boolean
        name:
            example: "Самый быстрый"
            type: string
        details:
            type: object
            additionalProperties: false
            required:
              - description
              - order_button
              - search_screen 
            properties: 
                ### строковое поле description уходит в пользу заголовка и 
                ### подзаголовка из нового дизайна, остальное остаётся так, как было
                description:
                    type: object
                    additionalProperties: false
                    required:
                      - title
                      - subtitle
                    description: описание тарифа
                    properties:
                        title:
                            type: string
                            example: "Несколько тарифов"
                        subtitle:
                            type: string
                            example: "Назначим ближайшую к вам машину"
                order_button:
                    type: object
                    additional_properties: false
                    required: 
                      - text
                    description: свойства кнопки заказа
                    properties:
                        text:
                            type: string
                            example: "Выберите минимум два тарифа"
                search_screen:
                    type: object
                    additionalProperties: false
                    required:
                      - title
                      - subtitle
                    description: свойства экрана поиска
                    properties:
                        title:
                            type: string
                            example: "Поиск"
                        subtitle:
                            type: string
                            example: "в нескольких тарифах"
        selection_rules:
            type: object
            additionalProperties: false
            required:
              - min_selected_count
            properties:
                min_selected_count:
                    type: object
                    additionalProperties: false
                    required:
                     - text
                     - value
                    properties:
                        text:
                            type: string
                            example: "Выберите не менее 2х тарифов"
                        value:
                            type: integer
                            description: минимальное количество выбранных классов                   
```

### Возвращение информации о мультиклассе в `/routestats`

Всю оставшуюся необходимую информацию о вертикалях можно вернуть в ответе `routestats`. 
Разместить её можно в соответствующей вертикали: 

```
GroupVertical:
    description: вертикаль для группировки тарифов
    type: object
    additionalProperties: false
    required:
      - type
      - id
      - tariffs
    properties:
        ...
        multiclass:
            description: |
                описание мультикласса (тариф "Самый быстрый") 
                для соответствующей вертикали
            $ref: "#/definitions/VerticalMulticlass"

UrlParts:
    description: url по частям
    type: object
    additionalProperties: false
    properties:
        key:
            type: string
        path:
            type: string

Image:
    description: картинка для клиента
    type: object
    additionalProperties: false
    properties:
        size_hint:
            type: integer
        url:
            type: string
        url_parts:
            $ref: "#/definitions/UrlParts"

VerticalMulticlass:
    type: object
    additionalProperties: false
    required:
      - tariffs
      - name
      - details
      - selection_rules
    properties:
        tariffs:
            descriptions: список тарифов для "Самого быстрого"
            type: array
            items:
                type: object 
                additionalProperties: false
                required:
                  - tariff
                  - selected          
                properties:
                    tariff:
                        type: string
                        description: название тарифа
                    selected:
                        type: boolean
        position:
            description: позиция в вертикали
            type: integer
        selector_icon:
            description: описание иконки в карточке "Самого быстрого"
            $ref: #/definitions/Image
        name:
            example: "Самый быстрый"
            type: string
        details:
            type: object
            additionalProperties: false
            required:
              - description
              - price
              - order_button
              - search_screen
            properties: 
                ### строковое поле description уходит в пользу заголовка и 
                ### подзаголовка из нового дизайна, остальное остаётся так, как было
                description:
                    type: object
                    additionalProperties: false
                    required:
                      - title
                      - subtitle
                    description: описание тарифа
                    properties:
                        title:
                            type: string
                            example: "Несколько тарифов"
                        subtitle:
                            type: string
                            example: "Назначим ближайшую к вам машину"
                price:
                    type: string
                    description: | 
                        Текст, содержащий цену и отображаемый на саммари.
                        Для "Самого быстрого" может быть составлен по отдельным правилам, 
                        поэтому возвращается в объекте мультикласса
                order_button:
                    type: object
                    additionalProperties: false
                    required: 
                      - text
                    description: свойства кнопки заказа
                    properties:
                        text:
                            type: string
                            example: "Выберите минимум два тарифа"
                        enabled:
                            type: boolean
                            description: | 
                                Сообщает, доступна ли кнопка заказа.
                                TODO: возможно, наличия сообщения о выборе тарифов достаточно, 
                                чтобы сделать вывод, что кнопка пока недоступна?
                search_screen:
                    type: object
                    additionalProperties: false
                    required:
                      - title
                      - subtitle
                    description: свойства экрана поиска
                    properties:
                        title:
                            type: string
                            example: "Поиск"
                        subtitle:
                            type: string
                            example: "в нескольких тарифах"
        selection_rules:
            type: object
            additionalProperties: false
            required:
              - min_selected_count
            properties:
                min_selected_count:
                    type: object
                    additionalProperties: false
                    required:
                     - text
                     - value
                    properties:
                        text:
                            type: string
                            example: "Выберите не менее 2х тарифов"
                        value:
                            type: integer
                            description: минимальное количество выбранных классов     
        estimated_waiting:
            type: object
            additionalProperties: false
            description: минимальное время ожидания для классов, входящих в "Самый быстрый"
            required:
              - message
              - seconds
            properties:
                message:
                    type: string
                    example: "2 мин"
                seconds:
                    type: integer   
        tariff_unavailable:
            type: object
            additionalProperties: false
            description: | 
                информация об ошибке, из-за которой мультикласс недоступен,
                например, нельзя выбрать при предзаказе или
                выбранном способе оплаты
            required:
              - code
              - message
            properties:
                code:
                    type: string
                    example: "multiclass_preorder_unavailable"
                message:
                    type: string
                    example: "Для этого тарифа нельзя запланировать поездку"
        unsupported_requirements:
            description: список неподдерживаемых пожеланий для выбранных классов
            type: array
            items:
                type: string
```

Поля `distance`, `time`, `time_seconds`, которые были в старом ответе мультикласса, 
можно взять из ответа `/routestats` - для мультикласса это те же значения.

### Изменения в запросе `/routestats`

#### Информация о выбранном флоу работы с мультиклассом

Клиент может поддерживать три способа работы с мультиклассом:
1. Один мультикласс в плоском списке тарифов.
2. Один мультикласс в вертикали - позиция мультикласса берётся из ответа `/zoneinfo`, 
а всё остальное - из мультикласса в `alternatives` в ответе `/routestats`.
3. Разные мультиклассы внутри разных вертикалей.

Клиент сможет правильно построить мультикласс для способа (3), 
если получен правильный сооответствующий ответ в zoneinfo 
(с необходимыми полями мультикласса в каждой вертикали). 

Чтобы не зависеть от возможных переключений эксперимента или ошибок при построении селектора в `/zoneinfo`, 
клиент будет передавать явный признак того, что мультикласс в каждой вертикали можно строить, в запрос `/routestats`:

```
RoutestatsRequest:
    additionalProperties: false
    properties:
        supported:
            description: список поддержанных опций
            type: array
            items:
                type: object
                additionalProperties: false
                required:
                  - type
                properties:
                    type:
                        type: string
...
```

#### Информация о выбранных классах

В запрос `/routestats` клиент отправляет информацию о выбранных пользователем тарифах в мультиклассе,
часть запроса выглядит так:
```
"multiclass_options": {
    "class": [
      "econom"
    ],
    "selected": true
  },
```

На первом этапе для упрощения разработки можно использовать имеющееся api.
Клиенты будут передавать все выбранные тарифы из всех "Самых быстрых" в поле `class`.
Тогда мультиклассы будут строиться из общих тарифов между вертикалями и выбранными тарифами.
Ограничение такого варианта: выбранный в одной вертикали тариф станет выбранным во всех вертикалях, где он есть.

На следующем этапе предлагается расширить `multiclass_options`, чтобы он влючал в себя и информацию 
о выбранных тарифах в вертикали. 
Нужно сохранять id вертикали, а поле `selected` не используется, и передавать его не будем, 
из `multiclass_options` тоже уберём.

Эта часть запроса будет выглядеть так:
```
multiclass_options:
    type: object
    additionalProperties: false
    description: информация о состоянии мультикласса на клиенте
    properties:
        class:
            type: array
            items:
                type: string
        verticals:
            type: array
            items:
                type: object
                additionalProperties: false
                description: информация о состоянии мультикласса в вертикали на клиенте
                required:
                  - vertical_id
                  - class
                properties:
                    vertical_id:
                        type: string
                        description: id вертикали
                    class:
                        type: array
                        items:
                            type: string
```
