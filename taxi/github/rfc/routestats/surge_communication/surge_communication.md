# Кастомизация информации о сурдже

## Что хотим

Провести эксперимент, в рамках которого для разных групп пользователей информация о повышенном коэффициенте будет
отображаться по разному. Предварительно будет кастомизироваться следующая инфа - цвет кнопки заказа, цвет и иконка
молнии, шторка (цвет/текст/кнопка) над адресами. В первой итерации необходимо поддержать возможность изменять цвета
кнопки заказа, цвета иконки сурджа, и саму иконку.

## Этап 0

Переводим управление отображением суржа на эксперименты 3.0. Примеры того, что надо уметь:

* нет суржа, никак не модифицируем интерфейс
* кнопку не красим, иконку красим, цвет иконки можно менять в экспе
* кнопку красим, иконку красим, цвета разные из экспа
* кнопку красим, иконку красим, цвета одинаковые из экспа
* кнопку не красим, иконку не рисуем

+ дополнительно: для п2-6 можем заменить иконку
+ в зависимости от коэффициента суржа, который приходит в эксперименте, мы можем совсем не показывать сурж в
  приложении (то есть в таком случае переходим в поведение в п1)

### API

В ручке 3.0/routestats для некоторых объектов `"service_levels"` планируется добавить новый ключ `"summary_style"`, в
котором будет содержаться информация о кастомизации элементов экрана. Вынесение иконок/заливок и пр. в отдельный объект
требуется для того, чтобы в дальнейшем упростить разработку новых фич, связанных со стилизацией.
![image](static/surge_communication.png)
![image](static/surge_communication_2.png)

Логика обработки на клиенте должна быть следующей:

* При наличии в ответе поля `"paid_options.display_card_icon": true` проверяем наличие
  ключа `"summary_style.surge_icon"`
  . Если он есть - информацию о типе, и цвете берем от туда, в противном случае оставляем дефолтное поведение.
* Аналогично для `"paid_options.color_button": true` - проверяем объект `"summary_style.order_button"` - если
  отсутствует
    - дефолтное поведение.

В первой итерации у `"color"` будет 2 возможных типа - `"solid"` (однотонный цвет) и `"linear_gradient"`. Значения
для `surge_icon.type` так же будут иметь фиксированный набор значений, какие именно - будет понятно когда принесут
дизайн. Сами иконки решили зашивать на клиенте, т.к. не планируется большого количества вариаций.

Пример ответа routestats:

```json
{
  "offer": "0713b6794f85db40d6dbe3b9559249f0",
  // ...
  "service_levels": [
    {
      "name": "Эконом",
      // ...
      "paid_options": {
        "value": 1.0,
        "display_card_icon": true,
        "show_order_popup": true,
        "color_button": true,
        "order_popup_properties": {
          "title": "",
          "comment": "",
          "description": "Нужно ОСАГО без ограничений",
          "reason": "Водитель может попросить показать полис ОСАГО. В поле «Лица, допущенные к управлению» должен стоять прочерк.",
          "button_text": "Хорошо, вызвать",
          "button_color": "38afff"
        },
        "alert_properties": {
          "label": "",
          "title": "",
          "description": "",
          "button_text": ""
        }
      },
      // New object in service_level
      "summary_style": {
        "surge_icon": {
          "color": "#fce006",
          "text_color": "#fce007",
          "background_color": "#fce008",
          "type": "default"
        },
        "order_button": {
          "text_color": "#hex",
          "fill": {
            "colors": [
              "#hex",
              "#hex"
            ],
            "type": "linear_gradient",
            // enum
            "positions": [
              1.0,
              1.1
            ],
            "angle": 360
          }
        }
      }
    }
  ]
  // ...
}
```

### Схема эксперимента

Подразумевается, что для различных групп пользователей будет возможность задавать различные диапазоны сурджей, для
каждого из которых будет возможность .

```yaml
name: surge_communications
type: experiment

value:
  schema:
    description: |
      Конфиг, в котором задаются комуникации с пользователем о сурдже (цвета кнопок, иконки и пр.).
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
        description: |
          Массив с со стилизацией компонент под различные диапазоны сурджей 
          по правилу surge_lower_bound <= surge < surge_upper_bound
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
              - background_color
              - type
              - text_color
            properties:
              show:
                type: boolean
                description: Показывать ли кнопку сурджа
              color:
                type: string
                description: HEX-код цвета иконки
              background_color:
                type: string
                description: HEX-код заднего фона за иконкой сурджа
              type:
                type: string
                description: Тип иконки
                enum:
                  - default
              text_color:
                type: string
                description: HEX-код цвета текста рядом с иконкой сурджа
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
              text_color:
                type: string
                description: HEX-код цвета текста внутри кнопки
              fill:
                $ref: '#/definitions/Fill'

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

### Реализация

На стороне бэкенда планируется изменить плагин surge в сервисе routestats, выполненный в рамках
задачи https://st.yandex-team.ru/EFFICIENCYDEV-11505. Этот экперимент в данный момент не проводится, функционал
полностью отдали нашей команде, поэтому конфликта интересов быть не должно. Поля `paid_options.display_card_icon`
, `paid_options.show_order_popup` и `paid_options.color_button` ответа routestats будут конфигурироваться экспериментом,
описанным выше. Для каждого пользователя из экспериментов будет приходить массив диапазонов сурджей, и стиль для каждого
из этих диапазонов.

Для стилизации компонент экрана добавится новый плагин summary_style, который будет возвращать цвета на основании того
же эксперимента и тех же проверок, что и surge. 