# Альтпины для точки Б

# Описание

Цель - снижение цены поездки.
Идея - давать пользователю альтернативную точку Б. Альтернативная точка будет в радиусе 500м (максимум) от желаемой, предлагаем пользователю пройти пешком.

- [Figma](https://www.figma.com/file/MXTTdbGkKPB3r71ftNK4DS/?node-id=1961%3A114561)
- [Project](https://st.yandex-team.ru/TAXIPROJECTS-3221)

![image](static/full.png)

# Продуктовые ограничения

## Доступность альтпина

Не даем возможность уехать с альтпином:

1. При заказе другому
2. При заказе с опциями (дети, перевозка животных)
3. Прибытие с 22:00 до 06:00
4. На тарифе самый быстрый
5. Если одна из точек (А или Б) - аэропорт / вокзал / автовокзал
6. При существовании активного заказа

## Пеший маршрут

Доступен во время поездки, и 10-15 минут после. Триггеры для остановки показа:

1. Пользователь нажал “Сбросить” (крайний справа скриншот)
2. Истекло допустимое время (10 - 15 минут после окончания поездки)

# API менеджера

## Бэкенд

1\. Включение всего флоу регулируется экспериментом `alt_point_switcher`. Иные эксперименты:  

  - altpin_settings - пачка трешхолдов для отдачи альтпина, уже настроен  

2\. Танкерные ключи (`backend.client_messages`) для построения модалки альтернативы в ответе `/3.0/routestats`:  

  - `altpin_b.confirmation_screen.title`
  - `altpin_b.confirmation_screen.modal.title`
  - `altpin_b.confirmation_screen.modal.description.subtitle`
  - `altpin_b.confirmation_screen.modal.close_button.text`
  - `altpin_b.confirmation_screen.modal.confirm_button.text`
  - `altpin_b.confirmation_screen.alternative_bubble.subtitle`
  - `origin_point_b.info_block.title`
  - `origin_point_b.info_block.subtitle`  

3\. Иконка человечка  

4\. Конфиги:
  - ALTPIN_MONEY_ZONES - пачка трешхолдов для отдачи альтпина, уже настроен
  - ALTPIN_B_ROUTE_AFTER_FINISH_TTL - сколько времени живёт маршрут после окончания поездки  

5\. tvm-правила:  

  - protocol -> alt, alt-b
  - api-proxy-critical -> alt, alt-b
  - api-proxy -> alt, alt-b
  - passenger-authorizer -> alt, alt-b

# Техническая реализация

## Клиент

### Альтернатива

![image](static/alternative.png)

Заводим новый тип альтернативы “altpin_b”

Содержимое = все то же самое что и в альтпине для точки А, а ещё:

1. Добавляем обязательное поле “badge” (”-40Р”) - показываем на саммари (при выбранной альтернативе) и на экране подтверждения

```yaml
Badge:
  type: object
  additionalProperties: false
  description: Бейдж на новой точке Б на саммари
  required:
    - text
    - text_color
    - color
  properties:
    text:
    	type: string
    	description: -40Р
    text_color:
    	type: string
    	description: HEX строка или color tag текста надписи
    color:
    	type: string
    	description: HEX строка или color tag фона бейджа
```

2. Добавляем обязательное поле “confirmation_screen” (см. описание ниже)
3. Расширяем “walk” обязательным полем “walk_time” (string). Используем его для отображения плашки на пешем маршруте.
4. Присылаем опциональное булево поле “service_levels[].order_for_other_prohibited” (уже есть обработка на клиентах, но по АПИ не используем). Если оно пришло и true, то заказ другому по данной альтернативе для данного тарифа невозможен. Реакция клиента аналогична реакции на обычный тариф с данным полем.

### Экран подтверждения

![image](static/confirmation.png)

Для альтернативы с “type”: “altpin_b” добавляется обязательное поле “confirmation_screen”.

**Содержимое экрана:**

Заголовок: поле confirmation_screen.title

Попап: поле confirmation_screen.modal

Бабл альтернативной точки: confirmation_screen.alternative_bubble

Бабл конечной точки: confirmation_screen.destination_bubble

```yaml
ConfirmationScreen:
  type: object
  additionalProperties: false
  description: Информация для экрана подтверждения выбора альтпина
  required:
    - modal
    - alternative_bubble
    - destination_bubble
  properties:
    title:
      type: string
      description: Заголовок вверху экрана

    alternative_bubble:
      description: Бабл альтернативной точки на карте
      schema:
        $ref: '#/definitions/ConfirmationScreenBubble'

    destination_bubble:
      description: Бабл конечной точки на карте
      schema:
        $ref: '#/definitions/ConfirmationScreenBubble'

    modal:
      description: Попап внизу экрана
      schema:
        $ref: '#/definitions/ConfirmationScreenModal'

definitions:
  Badge:
    type: object
    additionalProperties: false
    description: Бейдж на новой точке Б на саммари
    required:
      - text
      - text_color
      - color
    properties:
      text:
      	type: string
      	description: -40Р
      text_color:
      	type: string
      	description: HEX строка или color tag текста надписи
      color:
      	type: string
      	description: HEX строка или color tag фона бейджа


  ConfirmationScreenBubble:
    type: object
    additionalProperties: false
    required:
      - title
    properties:
      icon:
        type: object
        description: Иконка в бабле
        additionalProperties: false
        properties:
          image_tag:
            type: string
          image_url:
            type: string
      title:
        type: string
        description: |
        Заголовок бабла
        "Садовая-Спасская 1/2к7"
      subtitle:
        type: string
        description: |
          Подзаголовок бабла
          "В 15:33"
      badge:
        $ref: '#/definitions/Badge'

  ConfirmationScreenModal:
    type: object
    additionalProperties: false
    required:
      - title
      - buttons
    properties:
      title:
        type: string
        description: Заголовок в попапе
      description:
        description: Описание новой точки Б в попапе
        schema:
          $ref: '#/definitions/ConfirmationScreenModalDescription'
      buttons:
        description: Расположение и состав кнопок в модалке
        schema:
          $ref: '#/definitions/ConfirmationScreenModalButtons'

  ConfirmationScreenModalDescription:
    type: object
    additionalProperties: false
    required:
      - title
    properties:
      icon:
        type: object
        additionalProperties: false
        description: |
          Иконка слева
          Из image_tag/image_url приходит что-то одно
        properties:
          image_tag:
            type: string
          image_url:
            type: string
      title:
        type: string
        description: |
          Новая точка Б
          "Садовая-Спасская 1/2к7" на скрине выше
      subtitle:
        type: string
        description: |
          Текст в подазголовке
          "4 мин пешком" на скрине выше
      badge:
        $ref: '#/definitions/Badge'

  ConfirmationScreenModalButtons:
    type: object
    required:
      - orientation
      - items
    properties:
      orientation:
        type: string
        description: Ориентация кнопок в модальном окне
        enum:
          - horizontal
          - vertical
      items:
        type: array
        description: |
          Массив кнопок, показываемый слева на право или сверху вниз в зависимости от ориентации
        items:
          $ref: '#/definitions/ConfirmationScreenButton'

  ConfirmationScreenButton:
    type: object
    additionalProperties: false
    required:
      - text
      - text_color
      - color
      - action
    properties:
      text:
        type: string
      text_color:
        type: string
        example: '#000000'
      color:
        type: string
        example: '#000000'
      action:
        oneOf:
          - $ref: '#/definition/ConfirmAction'
          - $ref: '#/definition/CloseAction'

  ConfirmAction:
    type: object
    additionalProperties: false
    required:
      - type
    properties:
      type:
        type: string
        enum:
          - confirm

  CloseAction:
    type: object
    additionalProperties: false
    required:
      - type
    properties:
      type:
        type: string
        enum:
          - close
```

```json
{
  // ...
  "type": "altpin_b",
  "badge": {
    "text": "-40₽",
    "text_color": "#000000",
    "color": "#000000"
  },
  "walk": {
    "walk_time": "4 мин",
    "route": [ ... ]
  },
  "confirmation_screen": {
    "title": "Где закончится поездка",
    "alternative_bubble": {
      "title": "Садовая-Спасская 1/2к7",
      "subtitle": "В 15:33",
      "icon": {
        "image_tag": "alternative_bubble_icon_tag"
      },
      "badge": {
        "text": "-40₽",
        "text_color": "#000000",
        "color": "#000000"
      }
    },
    "destination_bubble": {
      "title": "Панкратьевский 12"
    },
    "modal": {
      "title": "Хотите выйти в другой точке и сэкономить 40 ₽?",
      "description": {
        "title": "Садовая-Спасская 1/2к7",
        "subtitle": "4 мин пешком",
        "badge": {
          "text": "-40₽",
          "text_color": "#000000",
          "color": "#000000"
        }
      },
      "buttons": {
        "orientation": "horizontal",
        "items": [
          {
            "text": "Нет, спасибо",
            "text_color": "#000000",
            "color": "#000000",
            "action": {
              "type": "close"
            }
          },
          {
            "text": "Да, хочу",
            "text_color": "#000000",
            "color": "#000000",
            "action": {
              "type": "confirm"
            }
          }
        ]
      }
    }
  }
}
```

### Пеший маршрут во время поездки

![image](static/ride_pedestrian_route.png)

Запрос к `/3.0/orderdraft` расшиярется опциональным полем `origin_point_b` (отдаётся, если заказ сделан по альтпину в Б):
```
{
  ...,
  "origin_point_b": {
    "geopoint": [double, double], // координаты изначально указанной тБ, если поездка сделана с использованием альтпина в Б
    "address": string // Строка, которую будем показывать ("До адреса *address*") после окончания поездки, но на этапе пешего маршрута
  }
  ...
}
```

Ответ `/3.0/taxiontheway` расширяется опциональным полем `origin_point_b`:
```
{
  ...,
  "origin_point_b": {
    "point": { // required
      "position": [double, double], // required
      "bubble": { // optional
        "text": "Панкратьевский пер. 12" // required
      }
    },
    "walk_time": "2 мин", // required
    "route": [ // required
      [
        37.82437232,
        55.75360465
      ],
      ...,
      [
        37.82284442,
        55.75428602
      ]
    ],
    "seconds_after_finish": int, // required
    "info_block": { // optional, приходит только в статусе complete
      "title": "Дальше 1 мин пешком", // required
      "subtitle": "До Панкратьевский пер. 12", // required
      "close_button": {
        "color": "#000000", // required
        "text_color": "#FFFFFF", // required
        "text": "Сбросить" // required
      }
    }
  }
  ...
}
```
Если клиент видет это поле, то отрисовывает маршрут согласно `route`.

Ответ `/3.0/launch` расширяется опциональным полем `orders_with_b_routes`:
```
{
  ...,
  "orders_state": {
    ...
    "orders": [
      {
        "orderid": "orderid1", // Активный заказ без альтофферов в Б
        ...
      },
      {
        "orderid": "orderid2", // Активный заказ с использованием альтоффера в Б
        ...
      }
    ]
  },
  "orders_with_b_routes": [
    {
      "orderid": "orderid2"
    },
    {
      "orderid": "orderid3" // Завершённый заказ с использованием альтоффера в Б
    }
  ]
}
```
В `orders_with_b_routes` приходят завершённые заказы, требующие построения пешего маршрута в данный момент. Если в ответе пришло поле `orders_with_b_routes`, то клиент для перечисленных в этом поле заказов также запрашивает `/3.0/taxiontheway`.


### Пеший маршрут после завершения поездки

![image](static/after_ride_pedestrian_route.png)

Всё точно также, как в предыдущем разделе. Но нужен эндпоинт для завершения показа вручную. Добавляем ручку `POST /4.0/pedestrian-route/cancel`:
**Request**
```
{
  "orderid": "orderid3"
}
```
**Response**
```
{
}
```
При неизвестной ошибке бекенда (т.е. при кодах, отличных от 200 и 404) показываем пользователю предупреждение об ошибке. На 404 реагируем забыванием пешего маршрута (стирем с экрана). Аналогично, если заказ пришёл в поле `orders_with_b_routes` ручки `/3.0/launch`, но поля `origin_point_b` в ответе `/3.0/taxiontheway` нет - останавливаем показ маршрута. Это означает, что уже прошло необходимое время с окончания поездки.

## Бэкенд

Функциональность считается некритичной. Поэтому при внутренних ошибках описанные выше поля могут и не вернуться (т.е. при ответе 200 от `/3.0/taxiontheway`, `/3.0/launch` корректная отдача информации по изначальной точке Б не гарантируется).

## Технические ограничения

Если с бэкенда приходит тип отображения кнопок `horizontal`, и количество кнопок более 2 - в приложении они должны отображаться вертикально.
