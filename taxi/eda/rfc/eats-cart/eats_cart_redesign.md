# Редизайн корзины
https://st.yandex-team.ru/RETAILSPECS-113 (см. итерация 2)

### Проблема:
Текущая корзина нам досталась от ресторанов, которые по своей специфике имеют в заказе в среднем 3-4 блюда, что не бьется с нашими закупочными заказами (от 14-30+ товаров в одной корзине).
Это влечет за собой невозможность нормально пользоваться корзиной, как одним из инструментов покупок. Поэтому было решено сделать редизайн корзины.

### Доработки на бэке:
1. Товары в подарок отображаем предпоследними в списке.
   - В CartItem есть поле promo_type - тип акции. Перед выдачей на фронт необходимо сдвинуть такие товары на места перед товарами которые недоступны.
2. Закончившиеся товары отображаем последними
   - В CartItem.MenuItem есть булевы признак available, который показывает доступность товара на данный момент. Если этот признак false, то такие товары сдвигаем в конец. 
   ### Варианты доработок по пунктам 1 и 2:
   1. По полю available и promo_type нужно написать компаратор, который отсортирует массив Cart.items перед выдачей на фронт.
      - Плюсы: проще и быстрее в разработке. 
      - Минусы: если появится потребность менять блоки местами, то придется переписывать код. 
      
   2. Завести конфиг 3.0 в котором можно указывать порядок расположения блоков (без акций и доступные, с акциями и доступные, не доступные).
      - Плюсы: если появится потребность менять блоки местами, то можно будет это сделать в эксперименте.
      - Минусы: сложнее и дольше в разработке.
   
   Было решено использовать вариант 1. Т.к сейчас нет продуктовой необходимости в таком конфиге. Если в будущем такая необходимость возникнет, то можно вернуться к варианту 2, поэтому оставлю схему конфига в документации.
   ### Схема конфига:
```
name: eats_cart_block_products
description: Управляет порядком сортировки в корзине Еды
type: config
value:
    schema:
        type: object
        additionalProperties: false
        required:
          - blocks
        properties:
            blocks:
                type: array
                items:
                    $ref: "#/definitions/blockItem"
                    
        definitions:
            blockItem:
                type: object
                required:
                  - block_type
                properties:
                    block_type:
                        type: string
                        enum:
                          - availiable
                          - promo
                          - not_availiable
```
   ### json конфига:
```
{
    "blocks":
    [
        {
            "block_type": "availiable"
        },
        {
            "block_type": "promo"
        },
        {
            "block_type": "not_availiable"
        }
    ]
}
```

3. Передавать признак "Товара нет в наличии".
   - Смотрим на признак available из п2. Сейчас этот признак всегда true, т.к eats-products не возвращает товары с available=false. Бэк будет отдавать товары с признаком available=false тоже. Фронты будут на него смотреть, и если он false, то писать на товаре "Разобрали".
     ## Доработки в eats-products:
     1. Из ручки `/api/v2/menu/get-items` возвращать и недоступные товары, если этот товар разобрали. При этом признак available=false. 
     2. Если товар вышел из ассортимента, то такой товар не возвращается на фронт.
     3. Отсутствие маппинга для товара: если нет маппинга, то eats-products не возвращает такие товары.
    
4. Скидки и акции.
   ### Проблема:
   В cart.items.place_menu_item.promo_types с бэка приходит массив [PromoType](https://a.yandex-team.ru/arcadia/taxi/uservices/services/eats-cart/docs/yaml/definitions/item.yaml?rev=r9020507#L115) - акции, которые применятся к данному товару при добавлении в корзину. В PromoType есть ссылки на картинки `picture_uri` и `detailed_picture_uri`, например в случае акции "Скидка для магазинов" это url на картинку с процентом. Хочется уйти от картинок в виде % для скидок. Для других акций в будущем тоже хочется от этого избавиться.

   ### Варианты решения:
   1. Вместе со ссылками на картинки передавать полноценный текстовый ответ с бэка для скидок, как это сделано сейчас в сервисе eats-products в ручке menu/goods. Для удобства и единообразия было решено применить схему PromoType из eats-products и в eats-cart тоже.
   ### Схема для PromoType:
```
    PromoType:
         description: Плашка скидки или акции
         oneOf:
           - $ref: '#/components/schemas/PriceDiscountPromoType'
           - $ref: '#/components/schemas/ProductPromoType'
         discriminator:
             propertyName: type
             mapping:
                 price_discount: '#/components/schemas/PriceDiscountPromoType'
                 product_promo: '#/components/schemas/ProductPromoType'
                 
    PriceDiscountPromoType:
         description: Скидка деньгами на товаре
         type: object
         additionalProperties: false
         required:
           - id
           - name
           - type
           - text
         properties:
             id:
                 type: integer
                 format: int64
                 description: Идентификатор типа акции
                 example: 2
             name:
                 type: string
                 description: Название типа акции
                 example: Скидка 10%
             pictureUri:
                 type: string
                 description: Изображение типа акции
                 example: https://eda.yandex/uploads/promos/5b73/5b73e9d999e2a.png
             detailedPictureUrl:
                 type: string
                 description: Изображение акции
                 example: https://eda.yandex/uploads/promos/5b73/5b73e9d999e2a.png
             text:
                 type: string
                 description: >
                     Текст акции для отображения на фронте
                 example: -10%
             type:
                 $ref: '#/components/schemas/PromoTypeType'
             badgeColor:
                 $ref: '#/components/schemas/Color'
             textColor:
                 $ref: '#/components/schemas/Color'

    ProductPromoType:
        description: Скидка товаром. Например, 1+1.
        type: object
        additionalProperties: false
        required:
          - id
          - name
          - type
        properties:
            id:
                type: integer
                format: int64
                description: Идентификатор типа акции
                example: 2
            name:
                type: string
                description: Название типа акции
                example: 1+1 халява рядом
            pictureUri:
                type: string
                description: Изображение типа акции
                example: https://eda.yandex/uploads/promos/5b73/5b73e9d999e2a.png
            detailedPictureUrl:
                type: string
                description: Изображение акции
                example: https://eda.yandex/uploads/promos/5b73/5b73e9d999e2a.png
            type:
                $ref: '#/components/schemas/PromoTypeType'
            badgeColor:
                $ref: '#/components/schemas/Color'
            text:
                type: string
                description: >
                    Ожидается что как минимум одно из 2х полей pictureUri или
                    text будет присутствовать в ответе. Если пришли оба
                    у text приоритет выше
            textColor:
                $ref: '#/components/schemas/Color'
                
    PromoTypeType:
         type: string
         description: >
             Тип плашки на товаре. Нужен, так как отображение на фронте отличается
               - price_discount: скидка деньгами (Пример: -15%)
               - product_promo: скидка продуктами (Пример: 1+1)
         enum:
           - price_discount
           - product_promo
          
    Color:
         type: object
         additionalProperties: false
         required:
           - light
           - dark
         properties:
             light:
                 type: string
                 description: Значение для светлой темы
             dark:
                 type: string
                 description: Значение для темной темы
             
```

2. Передавать два типа - с картинками (PromoTypeWithPictures) и  без картинок (PromoTypeWithText) в отдельном поле PromoTypeInfo, который будет находиться на уровне cart.items. При такой реализации нам не нужно помнить какие акции будут с картинками, а какие без картинок. Это будет разруливаться на бэке, в либе eats-disacount-applicator. 

### Схема для PromoType:
```
    PromoTypeInfo:
         description: Плашка скидки или акции
         oneOf:
           - $ref: '#/components/schemas/PromoTypeWithPictures'
           - $ref: '#/components/schemas/PromoTypeWithText'
         discriminator:
             propertyName: type
             mapping:
                 promo_type_with_pictures: '#/components/schemas/PromoTypeWithPictures'
                 promo_type_with_text: '#/components/schemas/PromoTypeWithText'
                 
    PromoTypeWithPictures:
         description: Тип акции с картинками, например "Скидка товаром: 1+1"
         type: object
         additionalProperties: false
         required:
           - id
           - name
           - pictureUri
         properties:
             id:
                 type: integer
                 format: int64
                 description: Идентификатор типа акции
                 example: 2
             name:
                 type: string
                 description: Название типа акции
                 example: 1+1 халява рядом
             pictureUri:
                 type: string
                 description: Изображение типа акции
                 example: https://eda.yandex/uploads/promos/5b73/5b73e9d999e2a.png
             detailedPictureUrl:
                 type: string
                 description: Изображение акции
                 example: https://eda.yandex/uploads/promos/5b73/5b73e9d999e2a.png

    PromoTypeWithText:
        description: Тип акции с текстом, например "Скидка деньгами на товаре"
        type: object
        additionalProperties: false
        required:
          - id
          - name
          - text
        properties:
            id:
                type: integer
                format: int64
                description: Идентификатор типа акции
                example: 2
            name:
                type: string
                description: Название типа акции
                example: Скидка 10%
            badgeColor:
                $ref: '#/components/schemas/Color'
            text:
                type: string
                description: >
                    Текст типа акции, например "%"
            textColor:
                $ref: '#/components/schemas/Color'               
          
    Color:
         type: object
         additionalProperties: false
         required:
           - light
           - dark
         properties:
             light:
                 type: string
                 description: Значение для светлой темы
             dark:
                 type: string
                 description: Значение для темной темы
             
```

Было решено использовать Вариант№ 2, т.к он выглядет логичней и не нужно думать в будущем где применять картинки, а где нет. 

   ### Конфиг для цвета текста и фона бейджа.
   В качестве конфига для настройки цветов фона и текста можно использовать конфиг из eats-products [EATS_CART_BADGES](https://a.yandex-team.ru/arcadia/taxi/schemas/schemas/configs/declarations/eats-products/EATS_PRODUCTS_BADGES.yaml).

   ### Доработки на фронтах:
1. Нужно поддержать новую схему PromoType с двумя типами - PromoTypeWithPictures и PromoTypeWithText.
   - В PromoTypeWithPictures будет передаваться pictureUri для отображения типа акции.
   - В PromoTypeWithText будут передаваться отдельными полями badgeColor и textColor для отображения типа акции.
