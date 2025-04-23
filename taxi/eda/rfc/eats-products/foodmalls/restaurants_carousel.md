# Двойная карусель для фудмоллов
PRD - https://wiki.yandex-team.ru/users/apykhtinn/foodmall/

### Проблема:
В ритейле появились фудмоллы в которых можно заказывать как еду, так и продукты. Сейчас у нас всего одна общая карусель категорий и в ней неудобно ориентироваться.

### Задача:
Для решения описанной проблемы в качестве быстрого решения нужно добавить вторую карусель с пипками, в которые на первый уровень категорий будет вынесены сами рестораны.

## Доработки в eats-nomenclature:
1. Завести в базе признак, что категория является рестораном.
2. В первой итерации проставлять этот признак руками в базе для категорий которые являются ресторанами.
3. Передавать этот признак в ответе категорий.

## Доработки в eats-products:
1. Расширить энам [CategoryShowIn](https://a.yandex-team.ru/arcadia/taxi/uservices/services/eats-products/docs/yaml/api/api.yaml?rev=r9645735#L361) еще одним значением `restaurants_carousel` - определяет, что категорию нужно отображать в карусели ресторанов.
2. `restaurants_carousel` проставляется тем категориям в ответе от номенклатуры для которых пришел признак `type` == `restaurant`
3. Расширить `payload` в [PostCatalogResponse](https://a.yandex-team.ru/arcadia/taxi/uservices/services/eats-products/docs/yaml/api/api.yaml?rev=r9645735#L591) объектом `carousel_mapping`.
4. `CarouselMapping` нужен для того, чтобы понимать какое имя будет у блока с данным `show_in` и какой порядок расположения будет у блоков. 

### Схемы:

```
CategoryShowIn:
    type: string
    enum:
      - banner_carousel
      - categories_carousel
      - horizontal_carousel
+     - restaurants_carousel
    description: >
        - banner_carousel: показывать в баннерах. Изображение
          для этого брать из gallery с соответствующим типом.
        - categories_carousel: показывать только в 
          карусели категорий ритейла.
          Изображение для этого брать из gallery с
          соответствующим типом.
        - horizontal_carousel: определяет, нужно ли отображать 
          категорию в виде горизонтальной карусели.
+       - restaurants_carousel: определяет нужно ли показывать 
+         категорию а карусели ресторанов.
+         Изображение для этого брать из gallery с
+         типом categories_carousel.
          
          
payload:
    type: object
    additionalProperties: false
    required:
      - categories
    properties:
        categories:
            type: array
            description: |
                Категории отдаются в сортированном порядке
                и от верхнего уровня (``parentId=null``) вниз
            items:
                $ref: '#/components/schemas/Category'
        features:
            type: array
            items:
                $ref: '#/components/schemas/Feature'
        communications:
            $ref: '#/components/schemas/Communications'
        goods_count:
            type: integer
            description: |
                Суммарное количество товаров во всех категориях
                после применения фильтрации
+       carousel_mapping:
+           description: |
+               Если не пришло, значит показываем 
+               только карусель категорий без заголовка.
+           $ref: '#/components/schemas/CarouselMapping'

CarouselMapping:
    type: object
    additionalProperties: false
    required:
        - carousels
    properties:
        carousel:
            type: array
            items:
                $ref: '#/components/schemas/Carousel'

            
Carousel:
    type: object
    additionalProperties: false
    required:
        - show_in
        - title
    properties:
        show_in:
            $ref: '#/components/schemas/CategoryShowIn'
            description: |
                Опеределяет, категории какого типа 
                показывать в карусели.
        title:
            type: string
            description: |
                Заголовок для карусели.
                Например: "Продукты"
                Управляется через танкер
```

5. Категории ресторанов не должны показываться в горизонтальных каруселях, в таком случае у них не должно быть `horizontal_carousel` в массиве show_in. 
   5.1 Сделать конфиг в котором будет регулироваться проставлять ресторанным категориям `horizontal_carousel` или нет.
6. `restaurants_carousel` нужно задавать через эксперимент по версии приложения. `horizontal_carousel` регулируется экспериментом `eats_products_horizontal_carousel_show_in` по версии приложения.

### Схема эксперимента:

```
name: eats_products_categories_carousels_position
type: experiment
description: Эксп, отвечающий за расположение каруселей.
value:
    schema:
        type: object
        additionalProperties: false
        required:
          - restaurant_carousel
          - categories_carousel
        properties:
            restaurant_carousel:
                type: integer
                description: 
                default: 0 
            categories_carousel:
                type: integer
                description:
                default: 1
```

## Доработки на фронтах:
1. Обрабатывать `carousel_mapping` и на его основе строить вторую карусель с ресторанами.
