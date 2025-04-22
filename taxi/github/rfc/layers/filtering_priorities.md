## Проблема
Хотим запихнуть на экран режима города (отдельная мода, экран дискавери) почти всё,
что есть в слоях: драйв, остановки, юзерплейсы, самокаты и еще потом рестораны планируются.

Много объектов из разных источников нужно фильтровать по-умному. Сейчас объекты из разных источников фильтруются независимо друг от друга.

## Что делаем
Делаем сравнение приоритетов посложнее:
Предлагается иметь кортеж приоритетов для каждого объекта. Состав приоритетов в кортеже и их
последовательность в нем задаётся конфигом. В качестве дефолта берём кортеж:

1) детерминированный хэш от айдишника объекта. Для примерно рандомного выбора равнозначных
объектов

При сравнении двух объектов хэш берется по модулю 1000 и делится на долю объектов провайдера сравниваемой фичи, чтобы фичи провайдера,
которых в ответе меньше, имели более высокую вероятность остаться на экране.

Для целей режима города хочется один из источников делать приоритетнее всех остальных,
чтобы его объекты не потерялись. В таком случае подойдет кортеж:

1) приоритет источника
2) приоритет типа объекта
3) приоритет по метаданным
4) хэш


```yaml
definitions:
    LayersPrioritiesConfig:
        type: object
        description: |
            конфиг для приоритезации объектов во время фильтрации. Настройки задаются для каждой пары (mode, screen)
        additionalProperties:
            description: screen
            type: object
            additionalProperties:
                $ref: '#/definitions/PrioritySettings'

    PrioritySettings:
        description: |
            Тут задаем содержимое кортежа приоритетов и конкретные значение для провайдеров
        type: object
        additionalProperties: false
        properties:
            priorities_tuple:
                type: array
                items:
                    $ref: "#/definitions/PriorityItem"
            debug_mode:
                description: Добавляет к фичам дебаг-информацию
                type: boolean
                default: false
        required:
          - priorities_tuple

    PriorityItem:
        description: Элемент кортежа приоритетов. Определяет логику, по которой получаем
            численное значение приоритета
        type: object
        additionalProperties: false
        properties:
            name:
                type: string
            payload:
                oneOf:
                  - $ref: "#/definitions/MultipliedHash"
                  - $ref: "#/definitions/ByFeatureMetaValue"
                  - $ref: "#/definitions/CustomValue"
                discriminator:
                    propertyName: type
                    mapping:
                        mult_hash: "#/definitions/MultipliedHash"
                        value: "#/definitions/CustomValue"
                        by_feauture_meta: "#/definitions/ByFeatureMetaValue"
        required:
          - payload
          - name

    MultipliedHash:
        description: |
            Сопоставляет объекту хэш, взятый по модулю 1000,  от id объекта, домноженный на заданное значение
        type: object
        additionalProperties: false
        properties:
            type:
                type: string
                enum:
                  - mult_hash
            by_provider:
                $ref: '#/definitions/IntegerMap'
        required:
          - type
          - by_provider

    CustomValue:
        description: |
            Конкретное значение приоритета, задаваемое руками
        type: object
        additionalProperties: false
        properties:
            type:
                type: string
                enum:
                  - value
            by_provider:
                $ref: '#/definitions/ByProviderCustomValue'
        required:
          - type
          - by_provider

    ByProviderCustomValue:
        description: |
            Здесь для провайдера задаём статичное значение приоритета
        type: object
        additionalProperties:
            $ref: '#/definitions/DefaultCustomValue'

    DefaultCustomValue:
        oneOf:
          - $ref: "#/definitions/CustomValueBySubType"
          - $ref: "#/definitions/ConstValue"
        discriminator:
            propertyName: type
            mapping:
                by_subtype: "#/definitions/CustomValueBySubType"
                const: "#/definitions/ConstValue"

    CustomValueBySubType:
        description: |
            Задаём значение приоритета в зависимости от подтипа объекта у провайдера
        type: object
        additionalProperties: false
        properties:
            type:
                type: string
                enum:
                  - by_subtype
            value:
                $ref: '#/definitions/IntegerMap'
        required:
          - type
          - value

    PriorityValue:
        type: integer
        minimum: 0
        x-taxi-cpp-type: std::size_t

    ConstValue:
        description: |
            Здесь задаём одно значение приоритета для всех объектов провайдера
        type: object
        additionalProperties: false
        properties:
            type:
                type: string
                enum:
                  - const
            value:
                $ref: "#/definitions/PriorityValue"
        required:
          - type
          - value

    IntegerMap:
        type: object
        additionalProperties:
            $ref: "#/definitions/PriorityValue"

    ByFeatureMetaValue:
        description: |
            Значение берется из мапы prioritizer_meta внутри фичи по ключу с дефолтом
        type: object
        additionalProperties: false
        properties:
            type:
                type: string
                enum:
                  - by_feauture_meta
            key:
                description: Какой ключ берем из мапы
                type: string
            default_value:
                description: |
                    Значение, которое подставляется, если указанного ключа нет
                $ref: "#/definitions/PriorityValue"
        required:
          - type
          - key
          - default_value
```

### пример

```json
{
  "city": {
    "discovery": {
      "priorities_tuple": [
        {
          "name": "object_type_priority",
          "payload": {
            "type": "value",
            "by_provider": {
              "stops": {
                "type": "by_subtype",
                "value": {
                  "shuttle_stop": 5,
                  "object": 1,
                  "__default__": 0
                }
              },
              "drive": {
                "type": "by_subtype",
                "value": {
                  "object": 1,
                  "cluster": 2,
                  "__default__": 1
                }
              },
              "__default__": {
                "type": "const",
                "value": 1
              }
            }
          }
        },
        {
          "name": "hash_with_multiplier",
          "payload": {
            "type": "mult_hash",
            "by_provider": {
              "stops": 1.5,
              "drive": 2,
              "scooters": 3,
              "__default__": 1.0
            }
          }
        }
      ]
    }
  }
}
```
