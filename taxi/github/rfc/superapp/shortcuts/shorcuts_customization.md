# Механизм управления внешним видом шорткатов

## Продуктовая задача

Управлять внешним видом шорткатов при помощи экспериментов.

Макет:
![Макет возможных кастомизаций внешнего вида шорткатов](./static/shortcuts_customization_mockup.png)

Что хочется уметь конфигурировать:
- Заголовок (`title`)
- Подзаголовок (`subtitle`)
- Текст бейджа (`text`)

Какие новые данные нужны:
- Цена поездки. См. подробную проработку [здесь](https://github.yandex-team.ru/privet/rfc/blob/feature/TAXIBACKEND-26901-offer-in-taxi-shortcut/superapp/shortcuts/taxi_offers.md). В силу сложностей реализации пока реализовано не будет.
- Рейтинг ресторана.
- Ценовая категория ресторана.

## Что уже есть

Смотри описание существующих экспериментов [тут](./experiments.md).

## Что предлагается сделать

### Изменение клиентского API
Для каждого объекта в масссиве `overlays` добавляется опциональное поле `attributed_text`:
```yaml
definitions:
    Link:
        additionalProperties: false
        properties:
            type:
                type: string
                enum:
                    - link
            link:
                type: string
            text:
                $ref: "#/definitions/Text"
        required:
            - type
            - link
            - text
        type: object
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
            meta_style:
                type: string
            text_decoration:
                description: |
                    описание значений (взято из text-decoration css):
                    * line_through - перечёркнутый текст
                    * underline - подчёркнутый текст
                type: array
                items:
                    type: string
                    enum:
                      - line_through
                      - underline
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
        required:
            - type
            - image_tag
        type: object

# ...
OverlayObject:
    type: object
    additionalProperties: false
    properties:
        # ...
        attributed_text:
            type: array
            items:
                oneOf:
                    $ref: "#/definitions/Link"
                    $ref: "#/definitions/Text"
                    $ref: "#/definitions/Image"
```

Изначально `attributed_text` содержал в себе только текст и картинки, однако время от времени появляется необходимость в использовании специфических сущностей (таких как неразделимые пробелы, ссылки и переносы строк). На старых клиентах это решалось использованием html внутри Text. Минусы html: 
* Отображение html на iOS из-за бага внутренней библиотеки даёт сбои

При наличии обоих полей `text` и `attributed_text` предпочтение отдаётся полю `attributed_text`. Предполагается, что клиент будет в том порядке, в котором перечислены параметры сложных объектов в массиве `attributed_text`, отрисовывать их на бейдже шортката.

#### Обратная совместимость

Для совместимости со старыми клиентами параметры текста в `attributed_text` также копируются в `text` и `text_color`. При наличии нескольких текстовых элементов в массиве `attributed_text` их содержимое конкатенируется и копируется в `text`, `text_color` при этом не заполняется.

### Эксперимент `superapp_shortcuts_badges`
Этот эксперимент консервируется, возможность задавать дефолтные настройки для бейджей переносится в эксперимент `superapp_shortcuts_content_settings`.

### Эксперимент `superapp_shortcuts_delivery_time`
Этот эксперимент консервируется, возможность задавать настройки времени доставки для шорткатов переносится в эксперимент `superapp_shortcuts_content_settings`.


### Новый эксперимент `superapp_shortcuts_content_settings`
Назначение эксперимента: разметка запросов для последующей кастомизации шорткатов

<details><summary>Схема эксперимента</summary>
<p>

```yaml
additionalProperties: false
definitions:
  TextTemplate:
    additionalProperties: false
    properties:
      text:
        type: string
      tanker_key:
        type: string
    type: object
  BadgeProperties:
    additionalProperties: false
    patternProperties:
      '\d+':
        $ref: "#/definitions/Badge"
      __default__:
        $ref: "#/definitions/Badge"
  Badge:
    additionalProperties: false
    properties:
      background:
        additionalProperties: false
        properties:
            color:
                type: string
        required:
            - color
        type: object
      shape:
        type: string
      tanker_key:
        type: string
      text:
        type: string
      text_color:
        type: string
      image_tag:
        type: string
  TaxiBadgeProperties:
    additionalProperties: false
    properties:
      __default__:
        $ref: "#/definitions/TaxiBadge"
      home:
        $ref: "#/definitions/TaxiBadge"
      work:
        $ref: "#/definitions/TaxiBadge"
  TaxiBadge:
    additionalProperties: false
    properties:
      background:
        additionalProperties: false
        properties:
          color:
            type: string
        required:
        - color
        type: object
      image_tag:
        type: string
      shape:
        type: string
    required:
      - background
      - image_tag
    type: object
      
properties:
    subtitle:
      additionalProperties: false
      properties:
        eats:place:
          $ref: "#/definitions/TextTemplate"
        grocery:category:
          $ref: "#/definitions/TextTemplate"
      type: object
    badges:
        additionalProperties: false
        properties:
          taxi:poi:
            $ref: "#/definitions/TaxiBadgeProperties"
          eats:place:
            $ref: "#/definitions/BadgeProperties"
          grocery:category:
            $ref: "#/definitions/BadgeProperties"
        required:
          - eats:place
          - grocery:category
        type: object
    delivery_times:
        additionalProperties: false
        properties:
            grocery:
              type: integer
        required:
          - grocery
        type: object
type: object
```

</p>
</details>

#### Как это работает
Эксперимент служит центральным местом для настроек содержимого шорткатов. Сюда из эксперимента `superapp_shortcut_badges` переносятся настройки дефолтного содержимого бейджа, а из `superapp_delivery_times` - возможность указать дефолтное время доставки для Лавки.

В составе эксперимента можно передать шаблон для подзаголовка и для текста бейджа. В шаблоне допустим параметр `{eta}`, при его наличии вместо него будет подставлено локализированное время доставки (по аналогии с тем, как это делается сейчас). Необходимо передать хотя бы одно из значений `text` или `tanker_key`. При наличии обоих приоритет отдаётся `tanker_key`.

Обращаю внимание, что значение, получаемое по ключу `tanker_key` (но, очевидно, не само имя ключа), также может содержать параметр `{eta}`.

### Новый эксперимент `superapp_shortcuts_content_customization_mark`


<details><summary>Схема эксперимента</summary>
<p>

```yaml
additionalProperties: false
properties:
    enabled:
        type: bool
    limit:
        type: integer
required:
    - enabled
    - limit
type: object
```

</p>
</details>


#### Как это работает

Этот эксперимент дёт возможность автору с помощью условий эксперимента разметить аудиторию, для которой будет изменён внешний вид шорткатов. А именно, предполагается, что для той части аудитории, для которой необходимо изменить внешний вид шортката, в теле эксперимента поле `enabled` будет равно `true`, а для остальных - `false`. `limit` - максимальное количество шорткатов в выдаче, вид которых нужно менять.


##### Зачем отдельный эксперимент?

Для удобства использования. Для возможности разметить аудиторию этот эксперимент должен иметь обычного консьюмера `shortcuts/shortcuts`. При этом добавить эти настройки, например, в `superapp_shortcuts_content_settings` было бы неудобно, т.к. тело у эксперимента одно, и, задавая для одной части аудитории `enabled=true`, а для другой `enabled=false`, пришлось бы (при наличиии) дублировать настройки подзаголовков и бейджей.

См. также описание работы эксперимента `superapp_shortcuts_content_customization`.

### Новый эксперимент `superapp_shortcuts_content_customization`
Назначение эксперимента: управление текстовым и другим визуальным содержимым шорткатов

<details><summary>Схема эксперимента</summary>
<p>

```yaml
definitions:
    Text:
        additionalProperties: false
        properties:
            text:
                $ref: "#/definitions/TextTemplate"
            # Другие поля см. в описании клиентского API
    Image:
        # См. описание клиентского API
    TextTemplate:
        additionalProperties: false
        properties:
            text:
                type: string
            tanker_key:
                type: string
        type: object

    # За исключением отсутствия шаблонов для `text` идентичен `OverlaysContent`
    # из клиентского API
    BadgeProperties:
        additionalProperties: false
        properties:
            background:
                additionalProperties: false
                properties:
                    color:
                        type: string
                        pattern: "^#[0-9A-Z]{6}"
                required:
                    - color
                type: object
            shape:
                type: string
            text:
                $ref: "#/definitions/TextTemplate"
            text_height:
                type: integer
            attributed_text:
                type: array
                items:
                    oneOf:
                        $ref: "#/definitions/Text"
                        $ref: "#/definitions/Image"
                type: object
        type: object
additionalProperties: false
properties:
    subtitle:
        $ref: "#/definitions/TextTemplate"
    badge:
        $ref: "#/definitions/BadgeProperties"
type: object
```

</p>
</details>

#### Как это будет работать
Отличие данного эксперимента от всех существовавших ранее в том, что в нём с помощью кваргов происходит фильтрация не свойств запроса (т.е., как правило, пользователя), а свойств шортката. Другими словами, при обработке запроса от пользователя этот эксперимент будет наполнять свои кварги и матчить свои условия на содержимое каждого отдельного шортката. Этот эксперимент будет иметь своего собственного консьюмера `shortcuts_content` и следующий набор кваргов:
```yaml
- name: shortcut_id
    type: string
    required: false
    whitelisted: true
- name: shortcut_scenario
    type: string
    required: false
    whitelisted: true
- name: eats_place_rating
    type: string
    required: false
    whitelisted: true
# cheap, moderate, expensive
- name: eats_place_price_category
    type: string
    required: false
    whitelisted: true
```

Поскольку матчить каждый шорткат в каждом ответе пользователю на условия этого эксперимента может быть непозволительно дорого, предлагается предварительно размечать аудиторию с помощью эксперимента `superapp_shortcuts_content_settings`. Таким образом, матчинг условий и изменение внешнего вида шортката будет происходить только для тех запросов, для которых в теле эксперимента `superapp_shortcuts_content_settings` поле `enabled` будет равно `true`, а кроме того, количество шорткатов, для которых может быть изменён внешний вид, будет ограничено значением `limit` из тела того же эксперимента. При отсутствии эксперимента `superapp_shortcuts_content_settings` изменение внешнего вида шорткатов происходить не будет.

Содержимое поля `badge_content` из тела эксперимента, при наличии, перекладывается в ответ клиенту с подстановкой параметров в текстовые шаблоны.

Например, для эксперимента
```json
{
    "badge": {
        "attributed_text": {
            "items": [
                {
                    "type": "image",
                    "image_tag": "ets_badge_icon",
                    "width": 15,
                    "vertical_alignment": "center",
                    "color": "#000000",
                },
                {
                    "type": "text",
                    "text": {
                        "text": "Еда: доставка за {eta}"
                    },
                    "font_size": 14,
                    "font_weight": "bold",
                    "font_style": "italic",
                    "color": "#000000"
                }
            ]
        }
    }
}
```
ответ клиенту будет выглядеть как
```json
{
    "overlays": [
        {
            "attributed_text": {
                "items": [
                    {
                        "type": "image",
                        "image_tag": "ets_badge_icon",
                        "width": 15,
                        "vertical_alignment": "center",
                        "color": "#000000",
                    },
                    {
                        "type": "text",
                        "text": "Еда: доставка за N минут",
                        "font_size": 14,
                        "font_weight": "bold",
                        "font_style": "italic",
                        "color": "#000000"
                    }
                ]
            }
        }
    ]
}
```


### Что отображаем
Для `subtitle`:
- `subtitle` из `superapp_shortcuts_content_customization`. Если его нет, то
- `subtitle` из `superapp_shortcuts_content_settings`. Если его нет, то подзаголовок отображаться не будет.

Для бейджа:
- `badge` из `superapp_shortcuts_content_customization`. Если его нет, то
- `badges` из `superapp_shortcuts_content_settings`. Если его нет, то бейдж отображаться не будет.

### Дополнительная конфигурация

Поскольку, как обозначено выше, матчить эксперимента на **все** шорткаты может быть непозволительно дорого, вводятся два конфига (имена условные)
- SHORTCUTS_CUSTOMIZATION_MATCH_LIMIT (значение по умолчанию 10)
- SHORTCUTS_CUSTOMIZATION_MAX_COUNT (значение по умолчанию 5)

Это значит, что для тех запросов, для которых с помощью эксперимента `superapp_shortcuts_content_settings` включена кастомизация шорткатов, мы максимум попытаемся сматчить условия эксперимента `superapp_shortcuts_content_customization` для 10 первых шорткатов, но при этом остановимся или после 10 попытки матчинга, или после того, как кастомизируем 5 шорткатов (или `limit` из эксперимента настроек, в зависимости от того, какое из двух значений меньше).

### Помимо экспериментов

Необходимо прокинуть данные для по ресторанам Еды для отображения в бейдже:
- Рейтинг ресторана
- Ценовая категория ресторана

Поскольку эти данные есть в таблицах, по которым генерируются снепшоты, загружаемые периодически на `eda-shortcuts`, достаточно добавить эти поля туда и пробрасывать их дальше.
