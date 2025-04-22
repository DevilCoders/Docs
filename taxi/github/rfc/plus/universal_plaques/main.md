# Гибкий шильдик

## Терминология
| Шильдик (состоит из множества виджетов) | виджет |
| --------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------: |
| <img src="https://jing.yandex-team.ru/files/arteeemik/Screenshot%202021-12-20%20at%2020.44.06.png" width="300">  | <img src="https://jing.yandex-team.ru/files/arteeemik/Screenshot%202021-12-20%20at%2020.51.59.png" width="300"> |
|   | <img src="https://jing.yandex-team.ru/files/arteeemik/Screenshot%202021-12-20%20at%2020.46.54.png" width="300"> |
|   | <img src="https://jing.yandex-team.ru/files/arteeemik/Screenshot%202021-12-20%20at%2020.46.41.png" width="300"> |
|   | <img src="https://jing.yandex-team.ru/files/arteeemik/Screenshot%202021-12-20%20at%2020.57.18.png" width="300"> |

## Предыстория
- Очень много логики про шильдик захордкожено на клиентах. Например, отступы виджетов друг от друга, их расположение, цвета и многое другое.


- Идея: проработать заранее все возможные варианты виджетов (самых маленьких частей, из которых может состоять шильдик), чтобы можно легко настраивать и создать шильдики под любые задачи.


## Полезные ссылки
Ссылка на figma (возможные вариации шильдика): https://www.figma.com/file/wbZR55DYhwpEQCL2GezUcm/Go-Плюс-II?node-id=3845%3A360102
Ссылка на Miro (хакатон описание задачи - гибкий шильдик): https://miro.com/app/board/uXjVOaVM-pE=/

## Изменения в API
Сейчас ответ ручки sdk-state выглядит следующим образом:
```yaml
{
  "state":
      $ref: "#/components/schemas/UserState"
  ...,
  "plaque": 
      $ref: '../definitions/plaque.yaml#/components/schemas/PlaqueDefinitions'
}
```
Где схема **PlaqueDefinitions** лежит здесь: [ссылка на API](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/uservices/services/plus-sweet-home/docs/yaml/definitions/plaque.yaml?rev=r8511031#L29)

В виду того, что структура шильдика кардинально изменится, то в ответе ручки sdk-state добавится поле **plaque_v2**:
```yaml
{
  "state":
      $ref: "#/components/schemas/UserState"
  ...
  "plaque": 
      $ref: '../definitions/plaque.yaml#/components/schemas/PlaqueDefinitions'
  "plaque_v2": 
      $ref: '../definitions/plaque.yaml#/components/schemas/PlaqueV2Definitions'    
}

PlaqueV2Definitions:
    type: object
    description: Описание шильдика V2.
    additionalProperties: false
    required:
      - widgets
      - plaques
      - widgets_levels
    properties:
        widgets:
            type: array
            description: |
                Список всех возможных виджетов
            items:
                $ref: '#/components/schemas/WidgetV2'
        plaques:
            type: array
            description: Список конечных шильдиков.
            items:
                $ref: '#/components/schemas/PlaqueV2'
        widgets_levels:
            type: array
            description: cписок уровней виджетов в шильдике
            items:
                $ref: '#/components/schemas/WidgetsLevel'
```

## Общая архитектура нового шильдика
- Сейчас шильдик формируется списком виджетов (на каждом уровне шильдика - один виджет).
- Новый шильдик будет формировать списком уровней, где на каждом уровне будет список виджетов. Виджеты будут максимально минимальными, чтобы  можно было максимально гибко формировать шильдик из виджетов.
- Добавится множество маленьких виджетов, параметров для виджетов (цвет, отступы, и т. д.)

## Логика про виджеты и их занимаемое место в шильдике:
1. Виджеты фиксированной длины занимают своё определенное пространство (fix и fit виджеты)
2. Потом если есть виджеты (не спейсеры) нефиксированной длины (fill виджеты) - занимают оставшееся место (длина всех уровней - максимальная длина уровня из списка уровней.).
3. Если место осталось, виджеты (спейсеры нефикс. длины) занимают оставшееся место

Высота виджета - максимальная высота одного из виджетов на этом же уровне

## Новые схемы
### Управление цветом
Цвет фона виджетов/кнопок будет управляться при помощи следующей схемы:
```yaml
Opacity:
    type: integer
    description: |
        Непрозрачность, где 0 - полностью прозрачный,
        100 - полностью непрозрачный.
    minimum: 0
    maximum: 100

Color:
    type: object 
    description: Параметры цвета - сам цвет и его позиция.
    additionalProperties: false
    required:
      - color
      - position
      - opacity
    properties:
      color:
          type: string
          example: "#00CA50"
          pattern: ^#[0-9A-Z]{6}
      position:
          type: number
          description: Возможные значения от 0 до 1.
          example: 0.5
          minimum: 0
          maximum: 1
      opacity:
          $ref: '#/components/schemas/Opacity'
          
Point:
    description: Относительные координаты [x, y] для раскраски фона шильдика, виджета, уровная и т.п.
    type: array
    items:
        type: number
    minItems: 2
    maxItems: 2
```

Пример линейного градиента
<img src="https://jing.yandex-team.ru/files/arteeemik/Screenshot%202022-01-27%20at%2017.36.57.png" width="400">
<img src="https://jing.yandex-team.ru/files/arteeemik/Screenshot%202022-01-27%20at%2017.52.11.png" width="400">

```yaml
ArrayColors:
    type: array
    description: |
        Массив из цветов.
        Если пришел массив из одного цвета - красим в один цвет
        Если пришло несколько - делаем градиентный цвет из элементов массива
    minItems: 1
    items:
      $ref: '#/components/schemas/Color'

LinearColorSettings:
    type: object 
    description: Настройки цветовой гаммы.
    additionalProperties: false
    required:
      - colors
      - start_point
      - end_point
    properties:
      colors:
          $ref: '#/components/schemas/ArrayColors'
      start_point:
          $ref: '#/components/schemas/Point'
      end_point:
          $ref: '#/components/schemas/Point'
            
RadialColorSettings:
    type: object 
    description: Настройки цветовой гаммы.
    additionalProperties: false
    required:
      - colors
      - central_point
    properties:
      colors:
          $ref: '#/components/schemas/ArrayColors'
      central_point:
          description: относительные координаты центра градиента. Под вопросом может ли центр иметь отриц и больше 1 значения координаты?
          $ref: '#/components/schemas/Point'

ColorSettings:
    type: object 
    description: Настройки цветовой гаммы.
    additionalProperties: false
    required:
      - type
    properties:
      type:
        type: string
        description: какой тип градиента - линейный или радиальный или полностью прозрачный.
        enum:
          - LINEAR
          - RADIAL
          - TRANSPARENT # прозрачный цвет
      linear:
        description: Придет, если тип LINEAR
        $ref: '#/components/schemas/LinearColorSettings'
      radial:
        description: Придет, если тип RADIAL
        $ref: '#/components/schemas/RadialColorSettings'
```

### Управление размером шильдика
- Обговорили, что делать scale сложно и теряется качество.


- На беке будет несколько настроек размеров шильдика в зависимости от модели устройства юзера: large, medium, small


- Бек будет присылать картинки разного размера в зависимости от того, какой размер шильдика нужен: large, medium или small


- Размером текстов: На беке будет информация о том, какой размер шильдика нужен(large, medium или small), и из размера шильдика из параметра текста font_size будет вычитаться определенное число (например, для large это число == 0, для medium == 2, для small == 4). 


- Все тексты в новом шильдике будут attributed_text


- Ширина шильдика будет определяться на клиенте самым большим размером уровня в шильдике


- Высота шильдика будет определяться на клиенте суммой высот каждого уровня в шильдике


### Поведение со старым шильдиков
Если пришло поле plaque_v2, то используем новые шильдики из plaque_v2. В этом случае не смотрим на plaque.
Если не пришло, то ориентируемся на данные из поля plaque.

### Новая схема шильдика
- Изменения с предыдущем шильдиком в поле widget_levels (раньше был список виджетов, теперь список уровней из виджетов).
- Еще добавил новый параметр display_rules
```yaml
PlaqueV2:
    type: object
    description: Конечный шильдик.
    additionalProperties: false
    required:
      - plaque_id
      - widgets_level_ids
      - condition
      - priority
      - display_rules
    properties:
        plaque_id:
            $ref: '#/components/schemas/PlaqueId'
        widgets_level_ids:
            type: array
            description: cписок уровней виджетов в шильдике
            items:
                $ref: '#/components/schemas/WidgetsLevelId'
        condition:
            $ref: '#/components/schemas/SimpleCondition'
        priority:
            type: integer
            description: |
                Приоритет, который необходимо будет присвоить шильдику,
                eсли удовлетворено условие показа.
                Если одним и тем же условиям удовлетворяют несколько
                шильдиков, то должен быть показан с наивысшим приоритетом.
        params:
            $ref: '#/components/schemas/PlaqueShowParams'
        display_rules:
            $ref: '#/components/schemas/DisplayRules'
        visual_effects:
            type: array
            items:
                $ref: '#/components/schemas/VisualEffect'
```

### Визуальные эффекты при действия с шильдиком (например, конфети)
```yaml
WidgetVisualEffect:
    type: object
    description: описание визуальных эффектов, которые могут возникать при действиях с виджетами в шильдике.
    additionalProperties: false
    required:
      - type
      - widget_id
    properties:
      type:
        type: string
        enum:
          - CLICK
      widgets:
        type: array
        items:
          $ref: '#/components/schemas/WidgetId'
      
VisualEffect:
    type: object
    description: Визуальные эффекты, которые могут применяться к шильдику.
    additionalProperties: false
    required:
      - type
      - trigger
    properties:
      trigger:
        type: string
        enum:
          - WIDGET            # Эффект, связанный с виджетами
          - OPEN_PLAQUE       # Открытие шильдика
          - SUCCESS_PURCHASE  # Успешная покупка подписки Яндекс.Плюс
      type:
        type: string
        enum:
          - CONFETTI
      widget:
        description: это поле будет в ответе, если тип визуального эффекта == WIDGET
        $ref: '#/components/schemas/WidgetVisualEffect'
```

### Визуальные параметры шильдика (display_rules)

####  Правила про несколько цветов в структуре ArrayColorSettings
Давайте договоримся, что в случае, если легко поддержать несколько градиентов (через поле ArrayColorSettings), то клиенты поддерживают. Если нет, то клиенты в случае, если пришло несколько цветов в поле ArrayColorSettings берут первый цвет и отрисовывают его. На другие элементы в массиве не смотрим.


Пример с отступами виджета:
<img src="https://jing.yandex-team.ru/files/arteeemik/Screenshot%202022-01-28%20at%2018.17.26.png" width="400">

```yaml
IndentRules:
    type: object
    description: |
      Параметры отступа от краёв (слева, справа, снизу, сверху). Измеряется в пунктах.
      Это поле есть у шильдика, уровня виджетов и самих виджетов. Работает для каждого компонента по следующим правилам:
          - Для шильдика: IndentRules - внутренние отступы. То есть все содержимое шильдика будет к границам не ближе чем указано в структуре IndentRules. При этом на фон шильдика это поле не влияет.
          - Для уровня виджетов: IndentRules - Тоже самое, что и для шильдика
          - Для виджета: тоже самое, что и для шильдика

    additionalProperties: false
    required:
      - indent_left
      - indent_right
      - indent_bottom
      - indent_top
    properties:
        indent_left:
            type: integer
        indent_right:
            type: integer
        indent_bottom:
            type: integer
        indent_top:
            type: integer
            
ArrayColorSettings:
  type: array
  minItems: 1
  items: 
    $ref: '#/components/schemas/ColorSettings'
    description: Массив градиентов/цветов. В несколько градиентов IOS может, андроид пока нет.

DisplayRules:
    type: object
    description: Настройки визуального отображения - отступы, цвета.
    additionalProperties: false
    required:
      - indent_rules
      - background_color_settings
    properties:
        indent_rules:
            $ref: '#/components/schemas/IndentRules'
        background_color_settings:
            description: |
              Цвет фона
            $ref: '#/components/schemas/ArrayColorSettings'
```

### Уровень виджетов
- У уровня виджетов тоже может быть свой цвет фона и дополнительные отступы, которые суммируются с граничными отступами для шильдика (сверху/справа/слева/снизу). Если поля не пришло, то стандартные отступы используем.
```yaml
WidgetsLevelId:
    description: имя уровня
    type: string
    example: balance_with_glyph

WidgetsLevel:
    type: object
    description: Конфигурация уровня - горизонтальный уровень виджетов.
    additionalProperties: false
    required:
      - widgets
      - widgets_level_id
      - display_rules
    properties:
        widgets_level_id:
            $ref: '#/components/schemas/WidgetsLevelId'
        widgets:
            type: array
            description: Список виджетов, из которых состоит уровень.
            items:
                $ref: '#/components/schemas/WidgetId'
        display_rules:
            $ref: '#/components/schemas/DisplayRules'

WidgetId:
    type: string
    description: Уникальный ID виджета.
```

### Новая схема виджетов

```yaml
DisplayWidgetRules:
    type: object
    description: Настройки отображения виджета.
    additionalProperties: false
    required:
      - width_type
      - display_rules
    properties:
      width_type:
          type: string
          example: fit|fill
          enum:
            - fit
            - fill
            - fix
          description: |
            fit - виджет заполняет только необходимое ему место (например, расширяется только на тот размер, чтобы уместился в него текст)
            fill - виджет занимает все доступное для него место (определяется по доступной свободной ширине на уровне в шильдике)
            fix - виджет заполняется пространство на определенное количество условных единиц в ширину. Количество будет указано в поле width_fix
      width_fix:
          type: integer
          description: Измеряется в пунктах. Ширина виджета (фиксированная). Это поле всегда должно приходить, когда тип width_type == fix.
      opacity:
          $ref: '#/components/schemas/Opacity'
          description: Для любого виджета мы должны уметь контролировать его прозрачность.
      display_rules:
          $ref: '#/components/schemas/DisplayRules'
      horizontal_rule:
            description: расположение содержание виджета по горизонтали. По умолчанию, если поля нет, по центру распологаем содержание.
            type: string
            enum:
              - LEFT
              - RIGHT
              - CENTER
      vertical_rule:
            description: расположение содержание виджета по вертикали. По умолчанию, если поля нет, по центру распологаем содержание.
            type: string
            enum:
              - CENTER
              - TOP
              - BOTTOM

WidgetV2:
    type: object
    description: Описание виджета - составной части уровня шильдика.
    additionalProperties: false
    required:
      - widget_id
      - type
      - display_widget_rules
    properties:
        widget_id:
            $ref: '#/components/schemas/WidgetId'
        display_widget_rules:
            $ref: '#/components/schemas/DisplayWidgetRules'
        type:
            type: string
            description: |
                Тип виджета - определяет его внешний вид.

                Описание конкертного типа располагается в поле,
                соответствующем названию типа (например, `button` для
                типа `BUTTON`).
            enum:
              - SPACER
              - BUTTON
              - SWITCH
              - BALANCE
              - TEXT
              - ICON
              - PROGRESS_BAR
        switch:
            $ref: '#/components/schemas/SwitchWidgetV2'
        button:
            $ref: '#/components/schemas/ButtonWidget'
        balance:
            $ref: '#/components/schemas/BalanceWidget'
        text:
            $ref: '#/components/schemas/TextWidget'
        icon:
            $ref: '#/components/schemas/IconWidget'
        progress_bar:
            $ref: '#/components/schemas/ProgressBarWidget'
        action:
            $ref: 'actions.yaml#/components/schemas/Action'
        templates:
            $ref: '../definitions.yaml#/components/schemas/Templates'
        widgets_level:  // Его пока что не делаем, держим в уме, что потом что-то похожее добавим
            $ref: 'compentnts/schemas/WidgetsLevel'
```

## Описание новых виджетов

### Пустой виджет
- Виджет нужен для того, чтобы пропускать место в шильдике, например, чтобы между виджетами была пустота, или заполнять пустоту с одной стороны и т. д.
- У пустого виджета будет только type, display_rules и widget_id. Тела у него не будет, так как туда нечего передать


### Прогресс Бар
<img src="https://jing.yandex-team.ru/files/arteeemik/Screenshot%202022-01-25%20at%2014.18.26.png" width="300">
Предлагаю для большей гибкости этот (в шильдике сверху) прогресс бар разделить на два виджета. В конфигах на беке он будет конфигурироваться как один, а на клиенты будет приходить как два виджета разных.

<img src="https://jing.yandex-team.ru/files/arteeemik/Screenshot%202022-01-25%20at%2014.18.33.png" width="300">

```yaml
ProgressBarLine:
    type: object
    description: прогресс бар в виде линии
    properties:
        text:
            $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
            example: 0/1
            
ProgressBarSettings:
    type: object
    description: Настройки для отображения прогресса в прогресс баре. По этим настройкам будет рисоваться прогресс по заданиям.
    additionalProperties: false
    required:
      - value
      - max
    properties:
        value:
            type: integer
            description: текущее значение по выполнению задания
        max:
            type: integer
            description: максимальное значение в прогресс баре

ProgressBarWidget:
    type: object
    description: Виджет - прогресс бар
    additionalProperties: false
    required:
      - type
      - color_successful
      - color_incomplete
      - settings
    properties:
        type:
            type: string
            description: |
                Тип прогресс бара.
            enum:
              - CIRCLE
              - LINE
        line:
            description: если не пришло поле, то будет просто линия выполнения задания
            $ref: '#/components/schemas/ProgressBarLine'
        color_successful:
            $ref: '#/components/schemas/ArrayColorSettings'
            description: цвет успешной линии в прогресс баре
        color_incomplete:
            $ref: '#/components/schemas/ArrayColorSettings'
            description: цвет невыполненной линии в прогресс баре
        settings:
            $ref: '#/components/schemas/ProgressBarSettings'
```

### Надвиджет над виджетом (о поле level_widgets)
Есть еще вот такой пример виджета
<img src="https://jing.yandex-team.ru/files/arteeemik/Screenshot%202021-12-22%20at%2014.16.27.png" width="300">

- Предлагаю у виджета сделать дополнительную поле - уровень виджетов. То есть у виджета будет еще уровень веджета, который будет отображается в уголку у виджета. Сможем настроить сразу там несколько элементов и действия на них.

### Остальные виджеты

```yaml         
ButtonWidget:
    type: object
    description: Виджет - кнопка.
    additionalProperties: false
    required:
      - text
    properties:
        text:
            $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
            description: Текст на кнопке.
            example: "Активировать"

Image:
    type: string
    description: url на изображение 

BalanceWidget:
    type: object
    description: |
        Виджет - текущее значение баланса.

        Значение баланса клиенты подставляют самостоятельно, используя
        кошелёк пользователя.
    additionalProperties: false
    properties:
        title:
            $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
            description: Текст над балансом.
            example: "ваши баллы"
        subtitle:
            $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'
            description: Текст под балансом.
            example: "баллов"
           
TextWidget:
    type: object
    description: Виджет - текст
    additionalProperties: false
    required:
      - text
    properties:
        text:
            $ref: 'extended-template/definitions.yaml#/definitions/AttributedText'

IconWidget:
    type: object
    description: Виджет - иконка
    additionalProperties: false
    required:
      - image
    properties:
      image:
          $ref: '#/components/schemas/Image'
          
SwitchWidgetV2:
    type: object
    description: Виджет - свитч (тогл).
    additionalProperties: false
    required:
        - text
    properties:
        text:
            $ref: '#/components/schemas/AttributedText'
            description: Текст рядом со свитчом.
            example: "Списать $$COMPOSITE_PAYMENT_AMOUNT$$ баллов"

```


Примеры json нового шильдика
| Шильдик |
| :---------------------------------------------------------------------------------: |
| <img src="https://jing.yandex-team.ru/files/arteeemik/Screenshot%202021-12-24%20at%2015.41.29.png" width="300"> |

```json
{
  "plaque_v2": {
    "plaques": [
      {
        "plaque_id": "plaque:taxi:catching_up_cashback:possible_cashback",
        "condition": {
          "screens": [
            "ride",
            "complete",
            "multiorder"
          ]
        },
        "params": {
          "show_after": 0
        },
        "priority": 2,
        "display_rules": {
          "background_color_settings": {
            "type": "LINEAR",
            "colors": [
              {
                "color": "#00CA50",
                "position": 0,
                "opacity": 100
              },
              {
                "color": "#FFFFFF",
                "position": 0.5,
                "opacity": 100
              },
              {
                "color": "#FFFAAA",
                "position": 0.75,
                "opacity": 100
              }
            ]
          },
          "indent_rules": {
            "indent_left": 4,
            "indent_right": 4,
            "indent_bottom": 4,
            "indent_top": 4
          }
        },
        "widgets_level_ids": ["level_possible_cashback_glyph_with_percent", "level_possible_cashback_text", "level_possible_cashback_button"],
        "visual_effects": [
          {
            "type": "WIDGET",
            "effect_type": "CONFETTI",
            "widget": {
              "type": "CLICK",
              "widget_id": "button_possible_cashback"
            }
          }
        ]
      }
    ],
    "widgets": [
      {
        "widget_id": "glyph",
        "type": "ICON",
        "display_widget_rules": {
          "width_type": "fit",
          "display_rules": {
              "background_color_settings": {
                "type": "LINEAR",
                "colors": []
              },
              "indent_rules": {
                "indent_left": 0,
                "indent_right": 0,
                "indent_bottom": 0,
                "indent_top": 0
              }
           }
        },
        "icon": {
          "image": "https://tc.tst.mobile.yandex.net/static/test-images/743/0085c8ffe4f54023b05822c7355ffa85"
        }
      },
      {
        "widget_id": "spacer",
        "type": "SPACER",
        "display_rules": {
          "width_type": "fill",
          "display_rules": {
              "background_color_settings": {
                "type": "LINEAR",
                "colors": []
              },
              "indent_rules": {
                "indent_left": 0,
                "indent_right": 0,
                "indent_bottom": 0,
                "indent_top": 0
              }
           }
        }
      },
      {
        "widget_id": "text_with_percent",
        "type": "TEXT",
        "display_rules": {
          "width_type": "fit",
          "horizontal_rule": "RIGHT",
          "display_rules": {
              "background_color_settings": {
                "type": "LINEAR",
                "colors": []
              },
              "indent_rules": {
                "indent_left": 0,
                "indent_right": 0,
                "indent_bottom": 0,
                "indent_top": 0
              }
           }
        },
        "text": {
          "text": {
            "items": [
              {
                "color": "#FFFFFF",
                "font_size": 30,
                "font_style": "normal",
                "font_weight": "medium",
                "text": "10%",
                "type": "text"
              }
            ]
          }
        }
      },
      {
        "widget_id": "text_possible_cashback",
        "type": "TEXT",
        "display_rules": {
          "width_type": "fit",
          "horizontal_rule": "RIGHT",
          "display_rules": {
              "background_color_settings": {
                "type": "LINEAR",
                "colors": []
              },
              "indent_rules": {
                "indent_left": 0,
                "indent_right": 0,
                "indent_bottom": 0,
                "indent_top": 0
              }
           }
        },
        "text": {
          "text": {
            "items": [
              {
                "color": "#FFFFFF",
                "font_size": 14,
                "font_style": "normal",
                "font_weight": "medium",
                "text": "баллами плюса\nза поездки",
                "type": "text"
              }
            ]
          }
        }
      },
      {
        "widget_id": "button_possible_cashback",
        "type": "BUTTON",
        "display_rules": {
          "width_type": "fit",
          "display_rules": {
              "background_color_settings": {
                "type": "LINEAR",
                "colors": []
              },
              "indent_rules": {
                "indent_left": 0,
                "indent_right": 0,
                "indent_bottom": 0,
                "indent_top": 0
              }
           }
        },
        "button": {
          "text": {
            "items": [
              {
                "color": "#FFFFFF",
                "font_size": 14,
                "font_style": "normal",
                "font_weight": "medium",
                "text": "Возвращать",
                "type": "text"
              }
            ]
          }
        },
        "action": {
            "type": "DEEPLINK",
            "deeplink": "yandextaxi://buy_plus"
          }
      }
    ],
    "widgets_levels": [
      {
        "widgets_level_id": "level_possible_cashback_glyph_with_percent",
        "display_rules": {
          "background_color_settings": {
            "type": "LINEAR",
            "colors": []
          },
          "indent_rules": {
            "indent_left": 0,
            "indent_right": 0,
            "indent_bottom": 4,
            "indent_top": 0
          }
        },
        "widgets": ["glyph", "spacer", "text_with_percent"]
      },
      {
        "widgets_level_id": "level_possible_cashback_text",
        "display_rules": {
          "indent_rules": {
            "indent_left": 0,
            "indent_right": 0,
            "indent_bottom": 0,
            "indent_top": 0
          },
          "background_color_settings": {
            "type": "LINEAR",
            "colors": []
          }
        },
        "widgets": ["text_possible_cashback"]
      },
      {
        "widgets_level_id": "level_possible_cashback_button",
        "widgets": ["button_possible_cashback"],
        "display_rules": {
          "indent_rules": {
            "indent_left": 0,
            "indent_right": 0,
            "indent_bottom": 0,
            "indent_top": 0
          },
          "background_color_settings": {
            "type": "LINEAR",
            "colors": []
          }
        }
      }
    ]
  }
}
```
