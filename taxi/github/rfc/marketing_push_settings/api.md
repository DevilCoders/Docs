## marketing push settings API

Предлагается переиспользовать принципы, заложенные в https://github.yandex-team.ru/taxi/rfc/pull/576, для отображения списка настроек со стороны бэкенда.

### /4.0/communications/push/settings

ListItem состоит из Lead и опционально Trail компонента и Action.
у Lead и Trail есть тип и далее опционально title, subtitle, icon_url. В title текст может передаваться строкой либо в терминах attributed_text, аналогично шорткатам.
Action состоит из типа и кастомного набора полей в зависимости от типа.

![push_settings](https://jing.yandex-team.ru/files/ihelos/Снимок%20экрана%202020-10-19%20в%2017.53.48.png)

**Запрос:**
```json5
{
  "position": [
    37.61763499999998,
    55.755821196486
  ],
   "push_settings": {
      "enabled_by_system": true, // включенность пушей в системных настройках
      // при изменении хотя бы одной настройки, клиенты отправляют весь итоговый стейт свитчеров
      "included_tags": ["new_functions"],
      "excluded_tags": ["drive_settings"]
   },
   "last_received_tags": ["grocery_news", "taxi_news"] // будет использоваться для дообновления списка, в случае если настроек нет в регионе 
}
```

**Ответ сервера:**
```json
{
  "menu": {
    "sections": [
        {
            "style": "default",
            "items": [
                {
                    "lead": {
                        "type": "default",
                        "title": {
                            "text": "О новых функциях"
                        }
                    },
                    "trail": {
                        "type": "switch"
                    },
                    "action": {
                        "type": "setting",
                        "content": {
                            "id": "new_functions",
                            "type": "push_setting"
                        }
                    }
                }
            ]
        },
        {
            "style": "bordered",
            "title": "Новости сервисов",
            "items": [
                {
                    "lead": {
                        "type": "default",
                        "title": {
                            "text": "Такси"
                        },  
                        "subtitle": {
                            "text": "Про новые тарифы"
                        }
                    },
                    "trail": {
                        "type": "switch"
                    },
                    "action": {
                        "type": "setting",
                        "content": {
                            "id": "taxi_news",
                            "type": "push_setting"
                        }
                    }
                }
            ]
        }
    ]
  }
}
```

```yaml
definitions:
    Menu:
        type: object
        description: Описание UI-струкутуры меню.
        additionalProperties: false
        required:
          - sections
        properties:
            sections:
                type: array
                items:
                    $ref: '#/definitions/Section'

    Section:
        type: object
        description: Описание секции в меню.
        additionalProperties: false
        required:
          - style
          - items
        properties:
            title:
                type: string
                description: Заголовок секции.
                example: "Кэшбэк в кафе"
            style:
                type: string
                description: |
                    Стиль оформления секции:
                    - `default` - простая секция
                    - `bordered` - секция с рамкой

                    Клиенты должны игнорировать неизвестные стили (фолбек - `default`).
                enum:
                  - default
                  - bordered
            items:
                type: array
                items:
                    $ref: '#/definitions/MenuItem'

    MenuItem:
        type: object
        description: Строка меню.
        additionalProperties: false
        required:
          - lead
        properties:
            lead:
                $ref: '#/definitions/MenuItemElement'
            trail:
                $ref: '#/definitions/MenuItemElement'
            action:
                $ref: '#/definitions/MenuItemAction'

    MenuItemElement:
        type: object
        description: Визуальный элемент строки меню.
        additionalProperties: false
        required:
          - type
        properties:
            type:
                type: string
                description: |
                    Стиль элемента:
                    - `default` - простой элемент с текстом
                    - `switch` - переключатель с двумя состояниями
                    - `nav` - элемент со стрелкой (по сути ссылка)

                    Клиенты должны игнорировать строки с неизвестными стилями.
                enum:
                  - default
                  - switch
                  - nav
            title:
                $ref: '#/definitions/TextTemplate'
                description: Основной текст элемента.
            subtitle:
                $ref: '#/definitions/TextTemplate'
                description: Подпись под основным текстом.
            icon_url:
                type: string
                description: URL c изображением, которое должно быть отображено в
                    элементе.

    TextTemplate:
        additionalProperties: false
        type: object
        properties:
            text:
                type: string
            attributed_text:
                $ref: "#/definitions/AttributedText"

    AttributedText:
        type: object
        additionalProperties: false
        required:
          - items
        properties:
            items:
                type: array
                items:
                    oneOf:
                      - $ref: "#/definitions/Text"
                      - $ref: "#/definitions/Image"

    Text:
        additionalProperties: false
        properties:
            type:
                type: string
                enum:
                  - text
            text:
                type: string
            font_size:
                type: integer
            font_weight:
                type: string
                enum:
                  - regular
                  - light
                  - medium
                  - bold
                  - display-heavy
            font_style:
                type: string
                enum:
                  - normal
                  - italic
            color:
                type: string
                pattern: "^#[0-9A-Z]{6}"
            meta_color:
                type: string
        required:
          - type
          - text
        type: object

    Image:
        additionalProperties: false
        properties:
            type:
                type: string
                enum:
                  - image
            image_tag:
                type: string
            width:
                type: integer
            vertical_alignment:
                type: string
                enum:
                  - baseline
                  - center
            color:
                type: string
                pattern: "^#[0-9A-Z]{6}"
            meta_color:
                type: string
        required:
          - type
          - image_tag
        type: object

    MenuItemAction:
        type: object
        description: Описание действия, которое должно быть выполнено.
        additionalProperties: false
        required:
          - type
          - content
        properties:
            type:
                type: string
                description: |
                    Тип совершаемого действия:
                    - `setting` - установка настройки
                    Клиенты должны игнорировать строки с неизвестными типами действий.
                enum:
                  - setting
            content:
                description: Описание данных для выполняемого действия.
                oneOf:
                  - $ref: '#/definitions/SetSettingAction'

    ### Actions
    SetSettingAction:
        type: object
        description: Описание действия - выставление настройки.
        additionalProperties: false
        required:
          - id
          - type
        properties:
            id:
                type: string
                description: Идентификатор настройки.
                example: "news"
            type:
                type: string
                description: |
                    Тип настройки:
                    - `push_settings` - настройки подписки
                enum:
                  - push_settings

```

**Способ вызова:**

Триггерить вызов /4.0/communications/push/settings только при нажатии на пункт "настройки" в боковом меню

Отображение пункта в боковом меню будет регулироваться экспериментом в launch:
 ```json5
 {
      "name":"push_settings",
      "value":{
        "enabled": true,
        "fallback_switcher": {
          "text": "some_key",
          "id": "__all__"
        },
        "l10n": {
          // ключи
        }
      }
    }
```

**фолбеки, на случай если settings не отвечает**:
- последний полученный ответ settings
- если последнего полученного ответа settings нет, то отобразить fallback_switcher из эксперимента push_settings


#### Детализация логики сохранения настроек на клиентах с учётом фолбэков:

Клиенты хранят у себя последний ответ ручки settings, чтобы показать настройки пользователю, если ручка не отвечает.
То есть fallback_switcher из эксперимента `push_settings` мы покажем пользователю только в том случае,
если он зашёл впервые в настройки пушей и в это время ручка settings была недоступна.

Если пользователь отключил пуши через fallback_switcher,
то `fallback_switcher.id` (`__all__`) сохраняется в массив `excluded_tags`
и потом отсылается на бэк при вызове launch / subscribe
(бэк его заменяет на список тэгов из эксперимента `marketing_push_fallback_tags`).

Если в `excluded_tags` был сохранён тэг фолбэка `__all__`, то при первом успешном ответе ручки `settings`
надо убрать этот тэг из `excluded_tags`, а все новые тэги, пришедшие в ответе ручки, сохранить в `excluded_tags`
(по-умолчанию при получении ответа ручки `settings` на клиенте все новые тэги сохраняются в `included_tags`)

### launch
по аналогии с /4.0/communications/push/subscribe в запрос добавляется отправка текущего локального стейта клиента:
```json5
{
    "push_settings": {
          "enabled_by_system": true, // включенность пушей в системных настройках
          // при изменении хотя бы одной настройки, клиенты отправляют весь итоговый стейт свитчеров
          "included_tags": ["new_functions"],
          "excluded_tags": ["drive_settings"]
    },
}
```

### /4.0/communications/push/subscribe

```json5
{
   "apns_type": "...",
   "push_tokens": {
     "apns_token": "...",
     "gcm_token": "...",
     "hms_token": "..."
   },
   "push_settings": {
          "enabled_by_system": true, // включенность пушей в системных настройках
          // при изменении хотя бы одной настройки, клиенты отправляют весь итоговый стейт свитчеров
          "included_tags": ["new_functions"],
          "excluded_tags": ["drive_settings"]
    },
}

```

ответ:
200
```json5
{}
```
