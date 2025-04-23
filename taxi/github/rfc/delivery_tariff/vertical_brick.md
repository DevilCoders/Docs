## Задача

Реализовать кирпичик вертикали на главном, 
переход по которому будет раскрывать тарифы из этой вертикали.

## Необходимые изменения

Кирпичик вертикали, в отличие от уже имеющихся, будет содержать новое поле `vertical_trap`.
Для кирпичика вертикали происходит редирект на саммари и выбирается тариф. 
Если `vertical_trap` будет иметь значение `true`, вертикаль развернётся в тарифы на саммари. 
Если нет - останется прежняя логика.

## Запуск mvp

Предполагается сделать изменение для пользователей с определённой версией iOs по аналогии с кирпичиком Доставки,
заменив для них кирпичик Транспорта на кирпичик вертикали Ультима. 
Сейчас кирпичик Доставки запущен под отдельным экспериментом `shortcuts_delivery_brick_availability`.
Кирпичик Ультимы можно запустить под аналогичным отдельным экспериментом `shortcuts_ultima_brick_availability`.
На этапе mvp решили не учитывать теги пользователей, а выгрузить список тех, кто использует Ультиму, и запускать на них.
Эксперимент будет по `phone_id`, зоне, платформе и версии.

## Детали реализации

Чтобы клиенты работали с кирпичиком вертикали привычным образом, он должен иметь тип `taxi:summary-redirect`.
Можно добавить новое значение в эксперимент `superapp_bricks_appearance` для Ультимы, аналогичное Доставке:
```
"taxi_header_ultima": {
    "class": "vip",
    "state": "collapsed",
    "icon_tag": "shortcuts_bricks_ultima",
    "vertical": "ultima",
    "vertical_trap": "true",
    "title_key": "superapp.ultima.service_name",
    "multicolor_icon": {
      "enabled_tag": "superapp_colored_brick_ultima",
      "disabled_tag": "superapp_colored_brick_ultima_disabled"
    },
    "background_color": "#F1F0ED",
    "active_text_color": "#000000",
    "disabled_text_color": "#AAAAAA"
  }
```

Доработки будут в сервисе `shortcuts`, в ответе ручки `/v1/blender-shortcuts`.

В ответ ручки в объект `TypedSummaryRedirectAction` также добавится опциональное поле `vertical_trap`:
```
TypedSummaryRedirectAction:
    type: object
    additionalProperties: false
    required:
      - type
    properties:
    ...
        vertical_trap:
            type: boolean
```