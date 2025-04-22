# Новый тип коммуникации Popup Helper

## Что хотим

В рамках эксперимента по отображению информации о сурдже добавить новый тип коммуникации с пользователем. Элемент
показан на рисунке ниже.
![image](static/popup_helper.png)

## Варианты реализации

Т.к. комуникация в данный момент предназначена только для показа в рамках эксперимента по повышенному коэффициенту,
одной из опцией является добавить информацию о плашке к ответу /routestats, `service_levels` к остальным объектам
данного эксперимента. Плюсы решения:

* Быстро сделать
* Легко поддерживать в рамках текущей задачи, т.к. весь связанный код находися в одном месте

Минусы:

* Фактически, коммуникация "прибивается гвоздями" в `service_levels`, за счет чего будет сложно ее переиспользовать
* Объекты коммуникаций будут разбросаны по разным ручкам, что приведет к усложнению их обработки на клиенте

Второй вариант - создать новый тип комуникации в сервисе inapp-communications. Плюсы:

* Можно переиспользовать компонент для проекта "Заказ другому"
* Не делаем временный код, который через какое-то время придется выкинуть

Минусы:

* Немного дольше и сложнее с точки зрения программирования

С прицелом на будущее решено делать второй вариант.

## Техническая реализация

В сервисе tariffs-promotions добавится новый промоблок PopupHelper, который будет показывать информацию об "помогающем
окне". Логика показа блока на текущем этапе будет следующей:

* Проверяем, попал ли клиент в группу эксперимента по "Зеленому режиму"
* Проверяем, пришло ли в запросе /inapp-communications поле `client_info.supported_configurations`, и наличие в нем
  ключа `dialogue.`
* Если да, достаем из редиса информацию по текущей калькуляции по всем тарифам, и сравниваем их сурдж с диапазонами в
  экспе.
* При выполнении условия surge_lower_bound <= current_surge < surge_upper_bound в ответе promos-on-summary будет
  возвращена информация по промоплашке, которая кастомизируется экспериментом.

Логика показа на клиенте:

* Фильтруем полученые промоплашки на основании текущего контекста (тарифкласс) и show_policy. Получается N (>=0)
  доступных промоплашек
* На свернутом саммари мы берем первую доступную промоплашку (они упорядочены согласно приоритетам). Если это dialog,
  отображаем сверху, если list то в свернутой карточке саммари.
* На развернутом саммари мы работаем со всеми доступными промоплашками. dialog отображаем только если он первый в
  доступных (остальные отбрасываем). list отображаем все.

Для отображения кнопки будет использоваться уже существующий виджет ActionButton. API и соотношение с элементами экрана
показано на рисунке ниже

![image](static/popup_helper_api.png)

Обновленная модель объекта, приходящего в `offers.promoblocks.items` представлена ниже

```yaml
PromoblockItem:
    type: object
    properties:
        id:
            type: string
        meta_type:
            description: |
                Поле для внутренней работы блендера. Игнорируется клиентами.
                inapp-communications также агрегирует внутри себя все промоблоки
                всех других источников и передаёт их клиентам.
            type: string
        # ... no changes
        widgets:
            type: object
            properties:
                # ...
                # Новый тип виджета, для которого будет использован существующий компонент бэка ActionButton.
                # Сейчас он используется, например, в компоненте /4.0/promotions/v1/promotion/retrieve Notification
                action_button: 
                    type: object
                    properties:
                        color:
                            type: string
                        text:
                            type: string
                        text_color:
                            type: string
                        deeplink:
                            type: string
                        action:
                            $ref: '#/definitions/WidgetAction'
            additionalProperties: false
        # ... no changes
        # Новое опциональное поле конфигурации 
        configuration:
            oneOf:
                - $ref: '#definitions/ConfigurationDialogue'
                - $ref: '...'  # тут будут новые типы конфигураций
            discriminator:
                propertyName: type
            
    additionalProperties: false
    required:
      - id
      - meta_type
      - supported_classes
      - title
      - widgets
```

## Эксперимент

Информация о попапе будет храниться в эксперименте по "Зеленому режиму", объекте popup_helper. В случае, если объект
отсутствует, пользователю не будет ничего показано. Структура экспа ниже:

```yaml
name: surge_communication
type: experiment

value:
  schema:
    description: Конфиг, в котором задаются комуникации с пользователем о сурдже (цвета кнопок, иконки и пр.).
    type: object
    additionalProperties: false
    required:
      - enabled
      - surge_treshold
      - surge_icon
      - order_button
    properties:
      enabled:
        type: boolean
        description: Включить/Выключить эксперимент
      display_info:
        type: array
        description: Массив с со стилизацией компонент под различные диапазоны сурджей по правилу surge_lower_bound <= surge < surge_upper_bound
        items:
          $ref: '#/definitions/DisplayInfo'

    definitions:
      DisplayInfo:
        type: object
        description: Конфигурация отображения элементов на экране
        properties:
          surge_lower_bound:
            type: string
            description: Нижний порог сурджа для попадания в правило
            pattern: '^[0-9]+(\.[0-9]{1,4})?$'
            x-taxi-cpp-type: decimal64::Decimal<4>
          surge_upper_bound:
            type: string
            description: Верхний порог сурджа для попадания в правило
            pattern: '^[0-9]+(\.[0-9]{1,4})?$'
            x-taxi-cpp-type: decimal64::Decimal<4>
          surge_icon:
            type: object
            additionalProperties: false
            required:
              - show
              - color
              - type
            properties:
              show:
                type: boolean
                description: Показывать ли кнопку сурджа
              color:
                type: string
                description: HEX-код цвета иконки
              type:
                type: string
                description: Тип иконки
                enum:
                  - default
          order_button:
            type: object
            additionalProperties: false
            required:
              - show
              - fill
            properties:
              show:
                type: boolean
                description: Показывать ли заливку кнопки для сурджа
              fill:
                $ref: '#/definitions/Fill'
          popup_helper:
            $ref: '#/definitions/PopupHelper'

    PopupHelper:
      type: object
      additionalProperties: false
      required:
        - color
        - text
        - text_color
      properties:
        text:
          type: string
          description: Текст на промоплашке
        text_color:
          type: string
          description: Цвет текста на промоплашке
        deeplink:
          type: string
        image_tag:
          type: string
          description: Тэг иконки, отображаемой на плашке
        background_color:
          type: string
          description: Цвет бэкграунда. Задается либо через hex, либо через ColorTag
        action:
          type: object
          properties:
            type:
              type: string
              enum:
                - deeplink
                - move
                - share
                - web_view
                - screenshare
            payload:
              oneOf:
                - $ref: '#/definitions/ActionPayload'
                - $ref: '#/definitions/MoveActionPayload'

      ActionPayload:
        type: object
        properties:
          content:
            type: string
          need_authorization:
            type: boolean
        required:
          - content
        additionalProperties: false

    MoveActionPayload:
      type: object
      properties:
        page:
          type: integer
        need_authorization:
          type: boolean
      required:
        - page
      additionalProperties: false

    Fill:
      type: object
      description: Описание цвета
      additionalProperties: false
      required:
        - type
      properties:
        type:
          type: string
          description: Тип цвета. Для "mono" обязательно задание параметра "color", для
            "linear_gradient" - "colors", "positions", "angle"
          enum:
            - solid
            - linear_gradient
        color:
          type: string
          description: HEX-код цвета
        colors:
          type: array
          description: Массив крайних цветов градиента, hex
          items:
            type: string
        positions:
          type: array
          description: Массив точек градиента
          items:
            type: string
            pattern: '^[0-9]+(\.[0-9]{1,2})?$'
            x-taxi-cpp-type: decimal64::Decimal<2>
        angle:
          type: integer
          description: Угол поворота градиента
```