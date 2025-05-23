### Описание
В рамках задачи по продаже алкоголя на самовывоз в алкомаркетах требуется отображать предупреждение о вреде алкоголя в карточках подробной информации о товаре.

### Ожидаемые изменения
Для реализации функциональности потребуется внести изменения в интерфейс взаимодействия сервиса eats-nomenclature, сервиса eats-products, а также в механизм взаимодействия с фронтами для поддержания возможности отображать блок текста без заголовка.

#### Изменения между eats-nomenclature и eats-products
Сервис eats-nomenclature должен добавить признак алкогольности в ответ ручки статической информации о товаре (`v1/products/info`).
В рамках спеки, способ, которым этот признак окажется в базе сервиса eats-nomenclature опускается, т.к. команда номенклатуры сама выберет способ решения задачи. Но концептуально это будет заключаться в том, что сотрудники контентного подразделения должны обработать все товары в алкомаркетах и для алкогольной продукции проставить в базу данных eats-nomenclature признак алкогольности.
В ручке `v1/products/info` в элементы массива `products` требуется добавить необязательное поле:

```
  is_alcohol:
      type: boolean
      description: Признак указывающий на то, что товар является алкогольной продукцией
      default: false
```

Сервис eats-products, при получении в ответе флага `is_alcohol`, должен добавлять текст о вреде чрезмерного употребления алкоголя и пробрасывать фронтам. 

#### Изменения между eats-products и фронтами
В ручке /api/v2/menu/product расшитить объект detailed_data новым типом блока `Note`

```
items:
    oneOf:
      - $ref: '#/components/schemas/Note'
```

Объект этого типа должен располагаться в свойстве note

```
mapping:
    note: '#/components/schemas/Note'
```

Структура нового объекта

```
        Note:
            type: object
            description: Блок текста несущий какую-либо информацию без заголовка.
            additionalProperties: false
            required:
              - type
              - payload
            properties:
                type:
                    type: string
                    enum: [note]
                payload:
                    type: object
                    additionalProperties: false
                    required:
                      - text
                    properties:
                        text:
                            type: string
                            example: Чрезмерное употребление алкоголя вредит 
                                вашему здоровью.
```

На фронтах объект указанного типа требуется отображать тем же стилем, что и свойство text в объектах description.

В eats-products добавить объект типа Note в поле, следующее после галереи картинок (сразу под картинками). В этом поле должен размещаться текст о вреде чрезмерного употребления алкоголя. 
Этот текст нужно взять из Танкера по ключу из конфига. Конфиг с этим полем должен быть добавлен в рамках RETAILSPECS-161, свойство warning, если на момент реализации конфиг еще не будет существовать - создать его.
Танкер потребуется добавить в сервис.
