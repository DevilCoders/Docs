# Промо-объекты над картой

## Продуктовая задача

У текущих промо-объектов, приходящих в слоях есть принципиальные проблемы с тем, что они показываются в неожиданных местах:
например, под шторой или за точкой А вверху, под пином, на карте, но за границами экрана.

При этом для нового года и 10-летия такси по эксперименту показывали промо-объект "прибитый" к экрану и это давало лучшую конверсию.
Хочется сделать универсальное решение, чтобы можно было их добавлять без перевыпуска клиента.

Новый вариант не является заменой для старых промо-обектов на карте, а дополняет его.

## Вариант решения

Добавляем в ответ `v1/products` новый блок `objects_over_map`, в котором будем присылать новые промо-обекты со следующими требованиями:

1. Расположения объектов строго фиксированы на экране и в одной части экрана не может отображаться более одного объекта.
2. Для объекта может приходить статичная картинка или векторная анимация lottie
3. По тапу на объект нужно уметь обрабатывать action'ы и/или диплинки
4. Нужна возможность добавлять подписи к объектам
5. Логика показов и анимаций регулирыется через show_policy
6. Анимации должны кэшироваться по той же логике, что и картинки и удаляться для уже проигранных анимаций (достигнуты лимиты в show_policy)
7. Клиент должен информировать бэкенд о показанных за сессию промо-объектов, чтобы не присылать разные промобъекты в соседних ответах.

## Изменения в протоколе

1. В ответ `v1/products` добавляется структура `objects_over_map` со следующим форматом

**YAML**
```yaml
properties:
  ...
  objects_over_map:
    type: array
    items:
      $ref: '#/definitions/ObjectOverMap'
  ...

definitions:
    ObjectOverMap:
      type: object
      additionalProperties: false
      required:
        - id
        - source
        - action
        - show_policy
        - position
      properties:
        id:
          type: string
        show_policy:
          $ref: '#/definitions/ShowPolicy'
        content:
          oneOf:
            - $ref: '#/definitions/LottieAnimation'
            - $ref: '#/definitions/StaticImage'
        action:
          $ref: '#/components/schemas/TypedAction'
        bubble:
          $ref: '#/components/schemas/AttributedText'
        position:
          type: string
          enum:
            - center_start
            - center_end
          description: положение объекта на экране, изначально поддерживаем только 2 - center_start (на 9 часов) и center_end (на 3 часа)
          
    LottieAnimation:
      type: object
      additionalProperties: false
      required:
        - type
        - source
        - count
        - delay
      properties:
        type:
          type: string
          enum:
            - animation
        count:
          type: integer
          description: число циклов анимации
        tap_count:
          type: integer
          description: число нажатий на объект, после которого прекращаем проигрывать анимацию
        delay:
          type: double
          description: задержка проигрывания анимации в секундах
        source:
          oneOf:
          - $ref: '#/definitions/LocalAnimation'
          - $ref: '#/definitions/RemoteAnimation'
    
    StaticImage:
      type: object
      additionalProperties: false
      required:
        - type
      properties:
        type:
          type: string
          enum:
            - image
        image_url:
          type: string
        image_tag:
          type: string
          
    LocalAnimation:
      type: object
      additionalProperties: false
      required:
        - type
        - name
      properties:
        type:
          type: string
          enum:
            - local
        name:
          type: string
      
    RemoteAnimation:
      type: object
      additionalProperties: false
      required:
        - type
        - url
      properties:
        type:
          type: string
          enum:
            - remote
        url:
          type: string
      

    ShowPolicy:
      type: object
      additionalProperties: false
      required:
        - id
      properties:
        id:
          type: string
        max_show_count:
          type: integer
```

Пример

**JSON**
```json
{
  "objects_over_map": [
    {
      "id": "some_promo_object",
      "content": {
        "type": "animation",
        "animation_count": 100,
        "tap_count": 10,
        "delay": 0.5,
        "source": {
          "url": "https://aws.com/mds/anitaion.json",
          "type": "remote" 
        }
      },
      "show_policy": {
        "id": "counter_id",
        "max_show_count": 5
      },
      "action": {
        "type": "deeplink",
        "deeplink": "yandextaxi://shortcuts"
      }
    }
  ]
}
```

2. В запрос `v1/products` в блок `state` добавляется список показанных в рамках текущей сессии промо-объектов `shown_objects_over_map`:

**YAML**
```yaml
properties:
  ...
  state:
    properties:
      ...
      shown_objects_over_map:
        type: array
        items:
          type: string
  ...
```